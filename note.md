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
- 