**会议主题** ：CloudWeGo 社区会议 12.14

**参会人** ：GuangmingLuo, welkeyever, YangruiEmma, Aster DY, whalecold, lvnszn, ylck, CoderPoet, li-jin-gou, Duslia, justlorain, HeyJavaBean, Feng Liang, baiyuntang, rogerogers, Skyenought, yinkehan, StellarisW, chaoranz758, ViolaPioggia, shiningstoned, Xiao Huang, Wang Yi, Ocyss_04, ahao, DMwangnima, XZ0730, Zhenting Zhang, Yichen Liu, cqqqq777

**会前必读** ：http://www.cloudwego.io/ ; https://github.com/cloudwego

### 议程一：Hertz [sse](https://github.com/hertz-contrib/sse) client 介绍 @ViolaPioggia

1. 项目描述：sse 协议是一种基于 HTTP 的应用层网络协议，用于服务端推送，基于 Eventstream 的事件流。官方文档：https://www.cloudwego.io/zh/docs/hertz/tutorials/basic-feature/protocol/sse/；GitHub 仓库：https://github.com/hertz-contrib/sse
2. 结果描述：
    1. 补充 Hertz sse client 侧代码，提供了监听服务端消息的能力。
    2. 提供了许多 Option 选项，可实现自定义如请求方法、请求头等功能。
    3. 完善优化了示例代码。
    4. 持续跟进新需求，如支持 POST 方法并携带 body。
3. 示例代码介绍。
4. 未来计划：补充客户端中断重连机制。

### 议程二：Hertz [websoket](https://github.com/hertz-contrib/websocket) 反向代理介绍 @justlorain

1. 基础知识：介绍了反向代理与 WebSocket。
2. 基本思路：通过 Hertz 提供 `http.Handler`，转发用户的 WebSocket 连接，最终实现代理服务器与真实服务器，用户与代理服务器的连接，代理服务器只负责消息转发。
3. 具体实现：源码位于 https://github.com/hertz-contrib/reverseproxy，实现步骤如下：
    1. 抽象 `WSReverseProxy` 主结构体，实现其构造方法 `NewWSReverseProxy`。
    2. 实现核心方法 `ServeHTTP`，主要分为以下四步：
        1. 准备请求头
        2. 代理服务器与后端服务器建立 WebSocket 连接
        3. 客户端与代理服务器建立 WebSocket 连接
        4. 连接通信
4. 示例代码：于 https://github.com/cloudwego/hertz-examples/tree/main/reverseproxy/websocket 提供了使用示例代码，并简单介绍。

### 议程三：Kitex [obs](https://github.com/kitex-contrib/obs-opentelemetry) slog 扩展介绍 @XZ0730

1. slog 简介：slog 是 Go 1.21 版本新增的结构化日志库，核心为 `Logger` 结构体和 `Handler` 接口。用户可以通过实现 `Handler` 接口实现自定义日志操作。
2. obs slog 扩展思路：
    1. 实现 Kitex `klog.FullLogger` 接口，使得 slog 适配 klog
    2. 自定义实现 `traceHandler`
    3. 在 `JSONHandler` 的基础上扩展 `Handle`方法，处理链路追踪的日志记录
3. Slog [More info](https://go.googlesource.com/proposal/+/master/design/56345-structured-logging.md)

### 议程四：一站式 RPC 调用介绍 @StellarisW

1. 背景：实现调用代码的自动化与平台化，用户更新 IDL 文件后由平台自动根据 IDL 文件生成代码，使得用户只需关心生成代码的仓库即可。
2. 架构：平台架构主要分为两部分，API 服务与 Agent 服务，API 服务充当调度器，通过一致性哈希算法下发任务到 Agent 服务，Agent 服务执行具体的任务。
3. 配置：用户只需配置 IDL 仓库、代码生成仓库与 token。
4. 存储：目前强依赖于 Mysql 用作元数据存储，Redis 用作服务注册与发现。但平台具有扩展性，可通过实现接口的方式来支持其他数据库。
5. 详细介绍了平台的基本使用。

### 议程五：[Dynamicgo](https://github.com/cloudwego/dynamicgo) 支持高性能 Protobuf 动态代理 @khan-yin

1. 背景：Dynamicgo 是字节跳动自研的高性能 Golang RPC 编解码基础库，用于实现**高性能 RPC 动态代理**场景；Protobuf 是一种跨平台、可扩展的序列化数据传输协议，目前有广泛应用。目前业界主流的 Protobuf 协议基础库并不能满足需求，故设计了高性能Protobuf 协议动态泛化调用链路。PR：https://github.com/cloudwego/dynamicgo/pull/37
2. Protobuf 设计思想：
    1. 官方源码链路思想：主要涉及三类数据类型之间的转换，以 Message 对象进行管理，自定义 Value 类实现反射和底层存储。
    2. Protobuf 编码格式：大体上遵循 TLV(Tag，Length，Value) 的结构，但针对具体的类型存在一些编码差异，主要有 Message Field、Message、List 和 Map 这几种类型。
    3. 源码 Descriptor 细节：不同的编码类型由不同的 Descriptor 描述，但 FieldDescriptor 兼容所有类型的描述。
3. 动态反射：借助 Go reflect 的设计思想，提供一套完整的反射 API。抽象了一个 TypeDescriptor 来表示更细粒度的类型。从协议本身的 TLV 嵌套思想出发，利用字节流的编码格式，建立健壮的自反射性结构体处理任意类型的解析。
4. 数据编排：借助 DOM （Document Object Model）思想，将原始字节流数据层层包裹的结构，抽象成多层嵌套的 BTree 结构，实现对数据的定位，切分，裁剪等操作的 inplace 处理。
5. 协议转换：介绍 Protobuf 与 JSON 相互转换的实现思路。
6. 性能测试：主要与 Protobuf-Go 官方源码进行比较，部分测试与 kitex-fast 也进行了比较。分别进行了反射、字段定量 Get/Set 与序列化/反序列化测试，测试结果均优于官方库。
7. 应用与展望：dynamicgo 还在持续迭代中，欢迎各位开发者参与，项目地址：https://github.com/cloudwego/dynamicgo

