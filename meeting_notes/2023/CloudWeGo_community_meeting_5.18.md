**会议主题** ：CloudWeGo 社区会议 5.18

**参会人** ：GuangmingLuo, goodbye-babyer, zhquzzuli, welkeyever, YangruiEmma, halst, whalecold, Cr., Haswf, li-jin-go, Joway, Duslia, FGYFFFF, ppzqh, Marina-Sakai , rogerogers , shiningstoned cqqqq777 , springrain

**会前必读** ：http://www.cloudwego.io/ ; https://github.com/cloudwego

### 议程一：云原生高性能内容平台 gpress 分享 @springrain

1. gpress 是一个云原生高性能内容平台，基于 Hertz + Go template + FTS5 ，对标 WordPress 。项目地址：https://github.com/springrain/gpress
2. 为何选择 Hertz ：
   1. 性能优秀，开发友好。
   2. cloudwego 社区活跃，提出的问题能得到及时解决。
   3. Hertz 的扩展性高，扩展成本低，方便引入如 GPRC 等微服务组件。
   4. Hertz 性能优秀。
3. 项目本质是利用去重优化的模式来实现的一个内容平台，可以自行编写一些模板主题来实现自定义场景。
4. gress 特点：
   1. gpress 直接兼容了 hugo 的模板，理论上来说 hugo 的模板几乎不用改动即可整体迁移到 gpress ，相较于 hugo 之类的静态网站，gpress 还支持全文检索。
   2. 部署容易。
   3. 基于去重理念开发，结构简单清晰，数据迁移容易，维护成本低。
   4. 自定义模板简单。
   5. 项目非常轻量级，对服务器压力小。
5. 遇到的问题：用户更换主题的需求。因为 Hertz 不支持对静态资源的动态加载，编写了 ReLoad 方法来解决资源加载问题，使用全局变量来控制当前使用模板，可以为开发者提供更友好的开发模板环境。

### 议程二：Hertz Recipes 进展介绍 @li-jin-gou

1. Client，RequestContext 与 Engine 这三个较重要文档中 Engine 文档已经完成，RequestContext 文档处于 pr 阶段，争取本周内完成。
2. Logger ，错误处理，SSE 已经完成,SSE 功能支持后用户逐渐增多。
3. 接受到用户的反馈，有一些文档仍需打磨和优化，后续还会补充其他的文档任务。
4. 仍有未认领的文档任务，呼吁大家积极参与社区建设。

