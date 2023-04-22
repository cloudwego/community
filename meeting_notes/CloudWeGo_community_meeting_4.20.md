**会议主题** ：CloudWeGo 社区会议 4.20

**参会人** ：GuangmingLuo, goodbye-babyer, zhquzzuli, welkeyever, YangruiEmma, halst, whalecold, Cr., Haswf, li-jin-go, Joway, Duslia, FGYFFFF, ppzqh, Marina-Sakai, Claude-zq, skyenought, rogerogers, L2ncE, Nihilism , Felix, shiningstoned, Yuqin425, cqqqq777

**会前必读** ：http://www.cloudwego.io/ ; https://github.com/cloudwego

### 议程一：kitex 新版本变更解读 @ppzqh

1. kitex 新版本，地址：https://github.com/cloudwego/kitex/releases/tag/v0.5.2
2. 在以往的 kitex 版本中针对超时都会有一个默认的重试，新版本中为重试添加了一个新的配置项，允许用户对超时默认不进行重试。
3. 在代码生成工具方面：支持了 windows 系统用户使用 kitex 生成代码。
4. RPC time out：在以往的版本中对超时的错误码只有一个 RPC time out 的超时，现在支持更细粒度的超时错误码，如可以分辨出在 context 中设置的 deadline 或 cancel 方法。
5. thrift fast codec：新增对 unknown fields 的序列化与反序列化。

---

### 议程二：shmipc-go 项目解读 & RoadMap 分享 @goodbye-babyer

1. shimpc-go 是一个基于共享内存来进行通讯的库，项目地址：https://github.com/cloudwego/shmipc-go
2. shimpc-go 背景：在字节内部落地 service mesh 架构的过程中，发现这种架构天然的会带来一些性能上的退化。在 service mesh 中是通过进程间的通讯去代理进程流量的，正常进程给间通讯是通过 Unix 的 socket 或 TCP 的 lookback 端口进行通讯，而在性能优化过程中想要再深入进行优化只能从一些基础的库考虑，其中比较显而易见的就是进程间的通讯这一方面，在业界中也有关于基于共享内存进行通讯的说法，但并没有统一的规范，而此项目便是在落地过程中就积累了大量的经验，在生产环境已经得到了较多使用，故开源出此项目来尽可能发挥出他最大的价值。
3. RoadMap：
   - 使用同样的规范去开源其他语言的 RPC 库，如 C++ ， Rust 。
   - 陆续将字节内部的实现移植到开源版本中。
   - 项目本身的持续技术迭代。

---

### 议程三：hertz-contrib/sse 扩展 @haswf

1. 项目地址：https://github.com/hertz-contrib/sse
2. 说明文档：https://bytedance.feishu.cn/docx/Kuk3dZLv2obwOpxUmW7cDvYEnLc

---

### 议程四：hertz-contrib/paseto 扩展 @Claude-zq

1. 项目地址：https://github.com/hertz-contrib/paseto
2. paseto 是为了解决 jwt 的安全问题而提出的新标准，官网：https://paseto.io/
3. 本项目采用了[go-paseto](https://github.com/aidantwoods/go-paseto)的一个实现，支持v2，v3，v4 这三个版本。
4. 源码解读：
   1. `func New(opts ...Option) app.HandlerFunc`：
      1. 根据参数获取配置。
      2. 根据配置中的 `KeyLookup` 决定获取从请求上下文的哪一部分获取 token 。
      3. 判断是否跳过 paseto 中间件。
      4. 根据配置判断是否去掉 token 前缀。
      5. 解析 token 。
      6. 将 token 放入请求上下文中。
   2. `Options` ：
      1. `Next` ：判断是否跳过此函数。
      2. `ErrorHandler` ：错误处理函数。
      3. `SuccessHandler` ：解析成功后的处理函数。
      4. `KeyLookup` ：决定从请求上下文的哪一部分获取 token 。
      5. `TokenPrefix` ：token 前缀，推荐使用 bearer 。
      6. `PraseFunc` ：解析 token 函数。
   3. extractors.go 文件：存放获取 token 的函数。
   4. generator.go 文件：存放生成 token 的函数，生成 token 有三个版本，两个模式，两个模式分别为 private 与 public ，private 使用对称加密，public 使用非对称加密。
   5. parser.go 文件：存放解析 token 的函数。

5. quick start：注册两个路由，第一个 GET 方法用于生成 token ，第二个 POST 方法用于核验 token ，开启一个协程，协程先获取 token ，后将 token 放入 header 中发送到服务器。
6. 在 FreeCar 2.0版本中将 jwt 替换成 paseto ，在 user 服务中申请 token ，采用的 v4 版本的 public 模式。