# 代码学习笔记

- [Viper](https://github.com/spf13/viper) 一个配置工具
- [Zap](https://github.com/uber-go/zap) 日志工具
- [gorm](https://gorm.io/gorm) 数据库工具


- 路由初始化:server/initialize/router.go
- server/middleware:中间件
    - server/middleware/casbin_rbac.go:鉴权
    - server/middleware/cors.go:跨域
    - server/middleware/email.go:邮件
    - server/middleware/error.go:处理panic
    - server/middleware/jwt.go:jwt
    - server/middleware/limit_ip.go:同一ip访问频率限制
    - server/middleware/loadtls.go:https
    - server/middleware/logger.go:日志?
    - server/middleware/need_init.go:数据库初始化
    - server/middleware/operation.go:操作日志?
- 中间件是在server/initialize/router.go中以Router.Use(middleware) 的方式调用的
- 鉴权:有一个casbin的策略,通过jwt就能确定是否有权调用api 可参见 [casbin](https://blog.csdn.net/weixin_51991615/article/details/123696937)
    - casbin似乎是通过如下的字符串来定义策略的
      ```casbin
      [request_definition]
      r = sub, obj, act
      
      [policy_definition]
      p = sub, obj, act
      
      [role_definition]
      g = _, _
      
      [policy_effect]
      e = some(where (p.eft == allow))
      
      [matchers]
      m = r.sub == p.sub && keyMatch2(r.obj,p.obj) && r.act == p.act
      ```

- 方便的入门资料 包括中间件和鉴权的一部分这里都有讲 [gin入门](https://blog.csdn.net/abcnull/article/details/122806028)
    - ```c.ShouldBindQuery(&struct{})``` query绑定struct
    - ```c.Bind(&struct{})``` form绑定struct
    - ```c.ShouldBindJSON(&struct{})``` json绑定struct
    - ```c.Json(200, struct{})``` struct转json
    - req/resp结构体中的tag
        - form/json/query
        - required：必填/omitempty：非必填
        - 