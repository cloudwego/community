**会议主题** ：CloudWeGo 社区会议 9.21

**参会人** ：GuangmingLuo, welkeyever, rogerogers, yiyun, whalecold, CoderPoet, HeyJavaBean, joway, Skyenought, felix021, baiyutang, L2ncE, li-jin-gou, FGYFFFF, jayantxie, ViolaPioggia, chaoranz758, Marina-Sakai, Ganlv, baize, Ocyss_04, tk_sky

**会前必读** ：http://www.cloudwego.io/ ; https://github.com/cloudwego

### 议程一：@林涵远分享 Kitex IDL 裁切工具项目进展与实现

1. 背景：IDL 仓库的不及时维护导致冗余内容增多，降低代码可读性，故 Thriftgo 在 v0.3.1 版本提供了 Thrift IDL 裁剪功能，用于减少冗余代码。
2. 裁剪原理：
	1. 遍历 IDL 文件将用到的 struct 标记为”有用“
	2. 扫描项目引用到的所有 IDL，保留被标记为”有用“的 struct，裁切掉未标记的
	3. 不对 IDL 中的 typedef、枚举和常数进行裁切
	4. 将裁切结果重新输出为 IDL 文件或生成 Golang 代码
3. 介绍 Trimmer 工具的使用以及如何在 Kitex Tool 中集成。
4. 后续规划：
	1. 支持多 IDL 联合裁切
	2. 保留字段定义顺序
	3. 优化裁切速度
	4. 为工具支持配置文件，增加在集成 Kitex Tool 时的参数设定
 
### 议程二：@FGYFFFF 分享 Hertz binding 重构

1. 背景：
	1. Hertz 使用的 “go-tagexpr” 库迭代过程中偶有 break，使得 Hertz 锁定在其 v2.9.2 版本
	2. 参数绑定是框架应用层的重要能力，Hertz 需要将其内敛以更好的满足需求
	3. “go-tagexpr” 适配标准库 HTTP 参数存储结构，Hertz 要使用其能力需大量调用 visitall() ，极端情况下性能劣化严重
2. 目标
	1. 重新实现参数绑定能力，完全自主可控
	2. 提高绑定性能
	3. 支持自定义绑定器与校验器
3. 设计思路：对每一个请求结构体类型进行缓存。在每一次请求进来时先查看是否存在缓存，如果存在则直接使用缓存信息，不存在则构建 & 缓存该类型的 decoder。
4. 前后对比：
	1. 参数绑定与验证行为未改变
	2. 重构参数绑定与校验配置行为，统一使用 WithOption() 方式注入配置
	3. 自定义 binder & validator
	4. 性能完全优于重构前
5. 介绍如何拓展 binder & validator。

### 议程三：@chaoranz758 分享 Hertz 文档优化和易用性的思路和效果展示

1. 补充缺失文档：补充 RequestContext 文档、Client 客户端文档与 HTTP 3 协议文档。
2. 文档优化：优化 Engine 文档、hz 文档、单测文档、文档代码示例、Link error 文档、用户反馈与网络库、协议库扩展文档。
3. 目录结构调整：合并流式处理文档，分散到 Engine 和 Client 中。将 hz 文档的目录展开，减少层级，优化用户体验。
4. 删除与 Hertz 无关的内容。

### 议程四：@rogerogers 分享 Hertz slog 的实现和应用

1. slog 是 go 官方提供的提供结构化日志记录的包，在 1.21.0 版本合入标准库，Hertz 的 hlog 已适配 slog。
2. slog 具备语法简介与配置较少，使用灵活与性能良好的优点，且位于标准库中，不用引入第三方包即可使用。
3. 介绍了 slog 的核心代码。
4. Hertz 适配 slog 中提供了设置日志等级、设置 slog Handler 与设置输出的 api。
5. 局限性：无法从 slog 实例中获取 handlerOptions，`SetOutput` 需要重建 logger 实例，目前直接使用的是 `JSONHandler`。

### 议程五：@GuangmingLuo 介绍 CWG 2周年 awesome contributor 的评选机制和敬请期待的大礼

1. 评选机制：基于 github 上的 pr、issue、push 等 action 的数量衡量贡献者，包括了 cloudwego、 Kitex contrib、Hertz contrib 以及 bytedance 仓库下的 Monoio、Sonic，统计时间为 2022.08.24～2023.08.24 。
2. 加分项：发布文章，参与 CSG 活动以及代表社区对外参加大会。
3. 贡献者分为年度突出贡献者、年度杰出贡献者与年度优秀贡献者，礼品分别对应为 PICO，科大讯飞电子阅读器，无线充电器，具体名单后续于公众号公布。
4. 将于十月二十一号下午在北京字节跳动工区举办线下活动，欢迎所有贡献者参与。
