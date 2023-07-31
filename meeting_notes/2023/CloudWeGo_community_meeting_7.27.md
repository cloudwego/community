**会议主题** ：CloudWeGo 社区会议 7.27

**参会人** ：GuangmingLuo, welkeyever, rogerogers, yiyun, YangruiEmma, liu-song, whalecold, CoderPoet, HeyJavaBean, Xuran, a631807682, joway, ExerciseBook, jasondeng1997, ppzqh, justlorain, Skyenought, hanyu, felix021, ii64, eric, cqqqq777

**会前必读** ：http://www.cloudwego.io/ ; https://github.com/cloudwego

### 议程一：@whalecold 分享 Kitex 支持 Nacos 配置中心实现原理和进展

1. 基本原理：Nacos 的 API 本身支持 watch 能力，Kitex 也提供了动态更新配置的机制，利用这两点下发 Nacos 的配置。
2. 使用：默认规定 dataId 的格式为 `${ClientServiceName}.${ServerServiceName}.${Category}`，也可自定义。在 Nacos 中按格式设置好配置后便会下发到服务。
3. 进度：已经实现客户端的超时重试和熔断策略，限流预计本月底完成。
4. 其他建议：提供类似 `WithBlock` 的选项让用户自主选择是否需要等待 Nacos 配置加载完成后才启动 client，在 Nacos 连通性出现问题时异步报错，不阻塞用户 client 的初始化。

### 议程二：@joway 分享 Kitex 在 k8s 环境下优雅停机最佳实践

1. 问题：在 K8s 部署架构下使用 Kitex 过程中经常会遇到连接断开，连接异常等等问题，这种问题部分情况下是 k8s 本身架构导致的。

2. k8s 服务注册与发现原理：

   1. 服务注册：当 k8s 的 pod 启动，通过 `readinessProbe` 的配置，定期检查 pod 是否已经准备就绪提供服务，当满足 `readinessProbe` 要求后，k8s 会将容器 IP 真正注册到 service 所属的健康 Endpoints 中，从而能够顺利的被服务发现。所以服务注册的关键在于 `readinessProbe` 的配置，比如一些服务可能启动后会做一系列的初始化操作才能正常提供服务，这是就需要定制化 `readinessProbe`。
   2. 服务发现：k8s 是通过 DNS 来做服务发现的。默认情况下，Cluster IP 全局唯一且不会随着后端的 pod 变化而变化，也就是说，Client 侧服务发现的结果永远只有一个 IP 地址。

3. 常见优雅停机的问题：

   1. Client 视角：

      问题：由于 Client 端永远只能发现一个 Cliuster IP，所以 Client 是无法感知到后端 pod 的变化的，也不存在摘除节点的操作。当下游节点开始销毁时，完全依赖 kube-proxy 即时删除 iptables 中对应的 pod IP，如果 kube-proxy 没有及时删除已经销毁的 pod IP，此时就有可能出现创建连接出现问题。

      解决方案：使用 k8s headless service。不再使用默认的 Cluster IP，要求每个 service 返回全量真实的 pod IP。

      问题：Client 的负载均衡是在创建连接时保持均衡，而发送的请求在不同连接的均衡依赖应用自己实现。如果 Client 时长连接，当下游节点增加 pod，上游一直没有建立新连接，那新节点可能迟迟无法收到足够多的流量，从而无法真正的负载均衡。

      解决方案：使用 k8s headless service；使用 Kitex 短连接

   2. Service 视角：

      k8s 只是提供了**可以实现优雅停机的能力**，但并不是直接部署的服务就直接具备此能力。

      当一个容器即将被关闭时，k8s 会做以下操作：

      1. 将该容器 IP 从 Service 的 Endpoints 中移除，这只保证新连接不会连接到此容器上，已存在连接不受影响
      2. 如果 pod 中有 container 配置了 preStop Hook，将执行 
      3. k8s 向容器进程发送 TERM 信号，Kitex 进行处理：
         1. 立即关闭当前监听的端口，已建立的连接不受影响
         2. 执行框架优雅停机逻辑
      4. 达到 k8s terminationGracePeriodSeconds 设置的超时时间，发送 KILL 信号强杀进程

      建议：开启 preStop Hook，并在其中执行 sleep 5s 左右的时间，以确保 kube-proxy 能及时通知上游不再对该 pod 建立连接

4. 思考：

   - 为什么 k8s 这么设计？

     k8s 是一个部署平台，提供了一些基础的能力，想要实现复杂的功能可以改造其组件

   - 真的能实现 100% 优雅停机吗？

     极端条件下，如请求处理时间 30s，默认情况下是不可能实现优雅停机的

   - 优雅停机问题的设计思想 

     框架/基础组件提供的是一种能力，服务应该利用此能力进行定制

