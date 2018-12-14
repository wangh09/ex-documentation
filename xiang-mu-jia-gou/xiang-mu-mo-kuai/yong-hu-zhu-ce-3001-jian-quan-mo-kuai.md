### 用户注册、鉴权 ink-uaa 模块

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
|    |            |     |_ JacksonConfiguration    json 配置
|    |            |     |_ LocaleConfiguration
|    |            |     |_ LoggingAspectConfiguration    
|    |            |     |_ LoggingConfiguration    
|    |            |     |_ MetricsConfiguration    监控配置 
|    |            |     |_ RedisConfiguration    redis 配置
|    |            |     |_ ThymeleafConfiguration    thymeleaf 配置
|    |            |     |_ UaaConfiguration    oauth2 授权配置，crsf权限配置、接口权限配置、401状态码返回配置
|    |            |     |_ UaaProperties    uaa 相关配置，鉴权token的clientId、secret、失效时间在此处配置
|    |            |     |_ UaaWebSecurityConfiguration
|    |            |     |_ WebConfigurer    CorsFillter 可以在此处配置
|    |            |
|    |            |
|    |            |__ domain    对应于数据库的实体类
|    |            |     |_ enumeration    枚举类
|    |            |     |_ AbstractAuditingEntity    复用类，继承该类将自动在事件生命周期自动执行相关操作。
|    |            |     |_ Authority    用户权限
|    |            |     |_ User    用户相关属性
|    |            |     |_ PersistentAuditEvent    记录相关网站操作事件
|    |            |
|    |            |
|    |            |__ repository    Spring Data JPA 的CRUD接口，自定义查询在该接口定义。
|    |            |
|    |            |
|    |            |__ security    安全相关
|    |            |     |_ AuthoritiesConstants    用户权限的常量设置
|    |            |     |_ DomainUserDetailsService    Gateway 登录时，会在该 service 进行鉴权，
|    |            |     |                              并创建 Authentication 的 principal 在 refreshToken .
|    |            |     |                              控制用户以什么样的方式登录获取鉴权在此处可以实现。
|    |            |     |
|    |            |     |_ IatTokenEnhancer    token签发自定义增强，token携带简短数据在此处自定义增强。
|    |            |     |                        
|    |            |     |_ SecurityUtils    实用工具栏，提供获取当前用户的 principal、用户是否登录、当前用户角色
|    |            |     |_ SpringSecurityAuditorAware
|    |            |     |_ UserNotActivatedException
|    |            |
|    |            |
|    |            |__ service    业务逻辑类
|    |            |     |_ dto    数据传输类
|    |            |     |_ impl    service 实现类
|    |            |     |_ mapper    Entity 和 DTO 转换接口
|    |            |     |_ util    工具包
|    |            |
|    |            |
|    |            |__ web.rest    API 接口
|    |                  |_ errors    API异常
|    |                  |_ util    工具包
|    |                  |_ vm    数据视图模型
|    |                  |_ AccountResource    用户注册、登录、更新、获取权限后登录(记录 IP)、用户信息、更改密码等
|    |                  |_ GoogleAuthenticate    创建 GA、更新 GA、GA 校验、GA 信息
|    |                  |_ SecurityCodeResource    用户资金安全密码创建、更新、校验、频率设置、频率状态
|    |                  |_ KycIntegrityResource    用户 KYC C1、C2、C3 认证校验、重新认证、认证状态、
|    |            
|    |-- resources    资源包
|           |_ config    配置文件
|           |    |_ liquibase
|           |    |      |_ changelog
|           |    |      |_ 000000000000_initial_schema.xml    项目初始文件
|           |    |            |_ timestamp_added_entity_EntityName.xml    实体类映射文件
|           |    |       
|           |    |_ master.xml    记录所有liquibase映射到数据库的文件
|           |    |_ users.csv    初始化的 user 数据
|           |    |_ authorities.csv    初始化的权限                                                                  
|           |    |_ users_authorities.csv    初始化的用户权限     
|           |    |_ bootstrap.yml     根配置文件 
|           |    |_ bootstrap-prod.yml     根配置生产环境文件 
|           | 
|           |_ i18n   国际化配置文件                       
|           |_ mails    邮件发送 html 模板
|           |_ templates    error.html 模板
|           |_ banner.txt    项目启动 banner
|
|____ pom.xml     maven 项目配置
```

---

##### 2.模块主要功能

1. Account 起始命名，实现用户注册、登录、更新功能。
2. Security 起始命名的，实现资金安全密码生成、重置、输入资金安全密码设置频率、频率状态和剩余时间功能。
3. IPRecords 起始命名的，实现用户登录 IP 记录
   1. **注：**API 接口目前只有一个，归到 Account API 内。
4. GoogleAuthenticate 起始命名的，实现用户绑定 GA 秘钥、重置 GA 秘钥、校验 GA、显示 GA 二维码、移除 GA （自动移除资金安全密码）功能。
   1. **注：**该功能所有数据操作均在 Security 数据库表中。
5. KYC 开头命名的，为用户 KYC 功能。
   1. KycIntegrityResource 归集了 C1/C2/C3 的认证、再次认证、认证状态功能。
   2. KycOne/Two/Three 起始命名的，实现了 C1/C2/C3 功能，现已归集。
6. UseResource 为管理员操作 API ，实现了增加、修改、删除用户等功能，后期为后台管理提供接口调用。

---

##### 3.项目启动

1. ./mvnw 启动默认 pom.xml 配置的环境。
   1. 启动别的环境执行 **./mvnw -Pdev   ./mvnw -Pprod  ./mvnw -Ptest**

---

##### 4.项目打包

1. mvn clean package -DskipTests=true -Pdev

2. mvn clean package -DskipTests=true -Pprod

3. mvn clean package -DskipTests=true -Ptest

4. 以上三个命令，自动打包前端页面。

---



