### 底层交易微服务 ink-service-ex-mapi 模块

---

##### 1.代码结构说明

```
|-- src
|    |-- main/java
|    |     |_ org.inklabsfoundation.inkapps     
|    |            |
|    |            |
|    |            |__ aop.logging    用于记录服务日志
|    |            |
|    |            |__ client    自定义增强客户端
|    |            |     |_ AuthorizedFeignClient    微服务模块之间权限调用客户端
|    |            |     |_ AuthorizedUserFeignClient    微服务模块之间权限调用客户端。
|    |            |     |                              （该客户端会携带用户 token ，使用场景较前者特殊一些）
|    |            |     |_ OAuth2InterceptedFeignConfiguration    oatuh2请求拦截器配置，验证从 Gateway 转发的服务是否合法。
|    |            |     |_ OAuth2UserClientFeignConfiguration     同下
|    |            |     |_ UserFeignClientInterceptor    user 客户端请求拦截器，用来校验从 Gateway 转发的服务是否合法。
|    |            |
|    |            |
|    |            |__ config    配置类       
|    |            |     |_ audit    事件组件
|    |            |     |_ ApplicationProperties    用来读取该模块在参配中心的 application 数据，使用 setter/getter 来获取。
|    |            |     |_ AsyncConfiguration    异步任务线程池配置    
|    |            |     |_ CacheConfiguration    缓存配置
|    |            |     |_ CloudDatabaseConfiguration    Cloud数据库配置
|    |            |     |_ Constants     配置项目常量
|    |            |     |_ DatabaseConfiguration    数据库配置，liquibase 读取 masste.xml 文件，进行校验。
|    |            |     |_ DateTimeFormatConfiguration    日期格式化配置，此处可以自定义 Converter
|    |            |     |_ DefaultProfileUtil    默认属性文件工具
|    |            |     |_ FeignConfiguration    Feign 配置
|    |            |     |_ JacksonConfiguration    json 配置
|    |            |     |_ LocaleConfiguration
|    |            |     |_ LoggingAspectConfiguration    
|    |            |     |_ LoggingConfiguration    
|    |            |     |_ MetricsConfiguration    监控配置 
|    |            |     |_ MicroserviceSecurityConfiguration    oauth2资源适配器，crsf权限配置、接口权限配置、401状态码返回配置
|    |            |     |_ RedisConfiguration    redis 配置 
|    |            |     |_ ThymeleafConfiguration    thymeleaf 配置
|    |            |     |_ WebConfigurer    CorsFillter 可以在此处配置
|    |            |
|    |            |
|    |            |__ domain    对应于数据库的实体类
|    |            |     |_ AbstractAuditingEntity    复用类，继承该类将自动在事件生命周期自动执行相关操作。
|    |            |     |_ DepositTrade    底层充值交易类
|    |            |     |_ SymbolRate    币种汇率类
|    |            |     |_ UserMatchRelation    Exchange Web 用户和底层用户映射类
|    |            |
|    |            |
|    |            |__ repository    Spring Data JPA 的CRUD接口，自定义查询在该接口定义。
|    |            |
|    |            |
|    |            |__ security    安全相关
|    |            |     |_ oauth2    oauth2 权限相关
|    |            |     |    |_ OAuth2SignatureVerifierClient    微服务模块验证客户端
|    |            |     |    |_ UaaSignatureVerifierClient    微服务模块验证客户端实现类，校验从 Gateway 转发的服务是否合法。
|    |            |     |
|    |            |     |
|    |            |     |_ AuthoritiesConstants    用户权限的常量设置
|    |            |     |_ SpringSecurityAuditorAware
|    |            |     |_ SecurityUtils    实用工具栏，提供获取当前用户的 principal、用户是否登录、当前用户角色
|    |            |
|    |            |
|    |            |__ service    业务逻辑类
|    |            |     |_ dto   
|    |            |     |_ impl  实现类
|    |            |     |_ mapper Entity 和 DTO 转换接口
|    |            |
|    |            |__ web.rest  API 接口
|    |                  |_ errors    API异常
|    |                  |_ util    工具包
|    |                  |  |_ CommonUtil   处理集合的通用工具类
|    |                  |  |_ CookieUtil   调用底层交易接口获取当前请求的相关cookie信息的工具类
|    |                  |  |_ HeaderUtil   微服务间调用请求头的处理工具类
|    |                  |  |_ TokenUtil    Gateway 转发微服务到该模块，获取当前用户 id，映射到底层账户 id，进行相关操作。
|    |                  |
|    |                  |
|    |                  |_ vm    数据视图模型
|    |                  |   |_ ApiAuthKeysUpdateVM    ApiKey更新视图
|    |                  |   |_ ApiAuthKeyVM           ApiKey视图               
|    |                  |   |_ BusinessOrder          订单视图
|    |                  |   |_ CancelOrder            订单取消视图
|    |                  |   |_ CurrencyVM             币种视图
|    |                  |   |_ DepositLogsVM          充值记录视图
|    |                  |   |_ LoggerVM               日志视图
|    |                  |   |_ MatResultUserVM        底层用户视图
|    |                  |   |_ MatUserVM              底层用户视图
|    |                  |   |_ OrderVM                订单视图
|    |                  |   |_ SpotAccountVM          账户视图
|    |                  |   |_ UserDTO                业务层用户视图
|    |                  |   |_ WithdrawAddressVM      提现地址视图
|    |                  |   |_ WithdrawBean           提现视图
|    |                  |   |_ WithdrawCoinVM         提现币种视图
|    |                  |   |_ WithdrawRequestCreateVM提现创建请求视图
|    |                  |   |_ WithdrawRequestVM      提现请求视图
|    |                  |   |_ WithdrawRuleVM         提现规则视图
|    |                  |
|    |                  |
|    |                  |_ DepositTradeResource    业务层添加充值交易开关功能
|    |                  |_ JsonResponse           异常封装
|    |                  |_ MatchAccountResource   底层账户的相关操作功能      
|    |                  |_ LogsResource    
|    |                  |_ MatchCommonResource    底层币种、币对的相关功能     
|    |                  |_ MatchFinanceResource    底层钱包充值规则、充值记录、币种充值信息、提现地址、提现记录等相关功能    
|    |                  |_ MatchTradeResource    查询订单相关信息功能
|    |                  |_ SymbolRateResource    币种费率功能、在 Gateway 实现（每3分钟）查询，写入数据库。
|    |                  |_ UserMatchRelationResource    底层账户和业务层账户对应关系相关功能     
|    |               
|    |                  
|    |            
|    |-- resources    资源包
|           |_ config    配置文件
|           |    |_ liquibase
|           |    |      |_ changelog
|           |    |      |_ 000000000000_initial_schema.xml    项目初始文件   
|           |    |_ bootstrap.yml     根配置文件 
|           |    |_ bootstrap-prod.yml     根配置生产环境文件 
|           | 
|           |_ i18n   国际化配置文件                       
|           |_ mails    邮件发送 html 模板
|           |_ templates    error.html 模板
|           |_ banner.txt    项目启动 banner
|    
|    
|    
|    
|____ pom.xml     maven 项目配置
         |_ 依赖于本地仓库，调用底层 client 及相关配置。 http://39.105.86.220:8080/repository/maven-public
```

---

##### 2.模块主要功能

1. DepositTradeResource  实现了业务层充值交易控制开关相关功能，后期会用到。
2. MatchAccountResource  实现了底层账户创建、更新、apiKey 的创建、关闭，获取个人账户等功能。
3. MatchCommonResource  实现了获取底层币种、币对相关信息的功能。
4. MatchFinanceResource  实现了获取底层币种充值规则、充值记录、充值地址、提现地址列表、提现记录、提现规则等功能。
5. MatchTradeResource  实现了条件查询订单信息、买卖盘、取消订单等功能。
6. SymbolRateResource  实现了币种汇率的固定刷新、币对汇率查询、法币和计价货币之间的转换等功能。（Gateway 外网查询，调用 mapi 实现该功能）
7. UserMatchRelationResource  实现了 Exchange Web 创建账户自动创建底层账户功能（在 Gateway register 调用），更新等功能。

---

#####  3.项目启动

1. ./mvnw 启动默认 pom.xml 配置的环境。
   1. 启动别的环境执行 **./mvnw -Pdev   ./mvnw -Pprod  ./mvnw -Ptest**

---

##### 4.项目打包

1. mvn clean package -DskipTests=true -Pdev

2. mvn clean package -DskipTests=true -Pprod

3. mvn clean package -DskipTests=true -Ptest

4. 以上三个命令，自动打包前端页面。



