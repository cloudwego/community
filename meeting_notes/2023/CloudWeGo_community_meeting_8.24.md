**会议主题** ：CloudWeGo 社区会议 8.24

**参会人** ：GuangmingLuo, welkeyever, rogerogers, yiyun, YangruiEmma, whalecold, CoderPoet, HeyJavaBean, joway, Skyenought, felix021, baiyutang, Sonui, StellarisW, L2ncE, li-jin-gou, sean.sun, lvnszn, FGYFFFF, liuq19, errocks, jayantxie, DMwangnima, ViolaPioggia, bobozhengsir

**会前必读** ：http://www.cloudwego.io/ ; https://github.com/cloudwego

### 议程一：@HeyJavaBean  分享 Kitex 新版本功能特性与变更 

1. gRPC 压缩支持：实现了 Kitex gRPC 的压缩功能支持，可以使用例如 gzip 等压缩方法减少 payload 的体积。
2. GLS：使用 local-session 组件兜底请求上下文，解决了用户没有传递 context 导致的微服务断链问题。
3. Unknown Fields 无序列化优化：实现无序列化的 unkonwn fields 功能，无序列化 unknown fields 方案在 FastCodec 上性能优化了约 6x~7x。详见：[#1017](https://github.com/cloudwego/kitex/pull/1017)
4. DynamicGO 集成：在 Kitex 的泛化模块中集成 dynamicgo 以提升 JSON/HTTP 泛化调用性能（+%50~200%）。
5. 升级 Thriftgo 库依赖至 v0.3.0，支持了 Thriftgo 反射功能，可以在运行时获取 IDL 元信息。

### 议程二：@bobozhengsir  分享 Volo 新版本功能特性与变更

1. Unknown Fileds：
   - Motivation：保留 Thrift 解码中未被识别的字段。
   - Solution：
     1. 在解码时，对未识别字段递归进行 skip 得到长度后，将等长度 bytes 存入生成的 _unknown fields 中，如果提前把已知字段读完，会直接把剩余 bytes 存储，不再解析长度。
     2. 在编码时，直接将 _unkonwn fields 整块写入，省去序列化的开销（volo 中是 zerocopy 实现）。
   - How To：在 volo.yml 中对要生成的 _unknown fields 的 thrift 文件进行配置
2. Binary Fast Skip：
   - Motivation：优化提示 Skip 逻辑的性能。
   - Solution：
     1. Thrift Binary Protocol Scalar Types 是定长编码，提前计算总长度来跳过，将 O(N) 的复杂度降到 O(1)。
     2. 使用循环替换递归。 
   - How To：升级至 Volo 最新版本。
3. Hot Restart：
   - Motivation：维护系统可用性、减少停机时间以及在升级过程中提供无缝的用户体验。
   - Solution：
     1. 初始化热重启机制。
     2. 尝试连接到 parent-sock。
        - 连接失败：该进程作为父进程绑定 parent_sock 和 parent_handle，等待子进程发消息。、
        - 连接成功：使用 dup_parent_listener_sock 复制文件描述符。
     3. 一旦所有监听器套接字都被复制，子进程向父进程发送终止请求，父进程收到后进行优雅退出。
   - How To：在 Server 启动前初始化 hot restart 即可。

### 议程三：@FGYFFFF  分享  cwgo hex 的代码生成及使用

1. 回顾 cwgo hex 的设计与实现，目前支持了在已有 RPC 服务上新增 HTTP 处理能力。
2. 视频演示 cwgo hex 的基本使用。
3. 主要逻辑：
   1. 继承 Kitex 原始的 transHandler，在其基础上实现协议嗅探，判断协议后下发请求。
   2. 初始化 hertz 的服务但是不主动监听端口，生成的 model 对齐 kitex_gen。

### 议程四：@王宇轩  分享 Kitex 支持 Dubbo 协议的进展和demo演示

1. 背景：Kitex 服务与 Dubbo （以 Dubbo Java 和 Dubbo Go 为主）的互通，RPC 协议需实现 Dubbo 协议，序列化协议主要支持 Hessian2，后续开发 Json 与 Protobuf。项目地址：https://github.com/kitex-contrib/codec-dubbo
2. 视频演示 Kitex 与 Dubbo Go 的互通。
3. 实现：
   1. RPC 协议：以 DubboCodec 为核心对象，实现 remote.Codec 接口，在 Encode/Decode 方法中完成 Kitex 与 Dubbo 调用模型的相互映射。
   2. 序列化协议：DubboCodec 利用 Hessian2 提供的 Encoder/Decoder，GetTypes/Response 完成 Dubbo（Java/Go type）、Hessian2、Kitex（thrift type）间的类型映射。同时借助 Kitex 生成的数据类型的 Encode/Decode 方法完成具体的数据序列化和反序列化。

### 议程五：@Guangming Luo  分享社区其他相关进展 & 组织 QA 讨论

1. 社区新增 Approver：https://github.com/cloudwego/community/issues/71
2. 官网新增 About 页面：https://www.cloudwego.io/zh/about/
3. 8月16号，社区与 CNCF 合作于新加坡，在新加坡理工大学纽约分校大楼举办了一场云原生技术沙龙，活动回顾：https://mp.weixin.qq.com/s/GctApXgKPkgC4jtPU1m0Sw
4. CloudWeGo 参加新加坡国立大学 2023 Orbital 暑期项目及优胜者颁奖典礼：https://mp.weixin.qq.com/s/gzXt8-9m9ZWo6aUhGEILRw

