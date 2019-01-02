### Web 网关 ink-gateway-ex-ui 模块

---

##### 1.代码结构说明

```
|-- src
|    |-- main/java
|    |     |_ org.inklabsfoundation.inkapps     
|    |            |
|    |            |
|    |            |__ aop.logging    记录服务日志
|    |            |
|    |            |
|    |            |__ config    配置类    
|    |            |     |_ apidoc     Gateway 的 Swagger 配置    
|    |            |     |_ audit    事件组件
|    |            |     |_ oauth2    oauth2 配置
|    |            |     |    |_ OAuth2AuthenticationConfiguration    实现了 oauth2 资源配置适配器，
|    |            |     |    |                                        接口授权、oatuh 2 鉴权、refreshToken 过滤器
|    |            |     |    |                                        (TokenExtractor)token提取器获取请求token
|    |            |     |    |_ OAuth2JwtAccessTokenConverter      自定义增强，用来处理 token 公钥 
|    |            |     |    |_ OAuth2Properties    oauth2 属性配置相关配置，鉴权token的clientId、secret、失效时间在此处配置
|    |            |     |
|    |            |     |_ ApplicationProperties    用来读取该模块在参配中心的 application 数据，使用 setter/getter 来获取。
|    |            |     |_ AsyncConfiguration    异步任务线程池配置    
|    |            |     |_ CacheConfiguration    缓存配置
|    |            |     |_ CloudDatabaseConfiguration    Cloud 数据库配置
|    |            |     |_ ClusterConfigurationPropertie     Redis集群属性
|    |            |     |_ ClusterRedisConfiguration         Redis Cluster 配置
|    |            |     |_ Constants     配置项目常量 （email、mobile 正则，redis key 头部，sms、email 模板名字，kyc 返回值）
|    |            |     |_ DatabaseConfiguration    数据库配置，liquibase 读取 masste.xml 文件，进行校验。
|    |            |     |_ DateTimeFormatConfiguration    日期格式化配置，此处可以自定义 Converter
|    |            |     |_ DefaultProfileUtil    默认属性文件工具
|    |            |     |_ GatewayConfiguration    Gateway Swagger、API Filter 访问过滤、API 访问速率配置
|    |            |     |_ JacksonConfiguration    json 配置
|    |            |     |_ LocaleConfiguration     系统环境变量、application、boostrap 等 yml 属性文件配置
|    |            |     |_ LoggingAspectConfiguration     LoggingAspect 配置   
|    |            |     |_ LoggingConfiguration    logstash 配置
|    |            |     |_ MetricsConfiguration    监控配置 
|    |            |     |_ MicroserviceSecurityConfiguration    oauth2资源适配器，crsf权限配置、接口权限配置、401状态码返回配置
|    |            |     |_ RedisConfiguration    redis signle 配置
|    |            |     |_ ThymeleafConfiguration    thymeleaf 模板引擎配置(email 使用)
|    |            |     |_ WebConfigurer    CorsFillter 可以在此处配置
|    |            |
|    |            |
|    |            |__ domain    对应于数据库的实体类
|    |            |     |_ enumeration    枚举类
|    |            |     |_ AbstractAuditingEntity    复用类，继承该类将自动在事件生命周期自动执行相关操作。
|    |            |     |_ PersistentAuditEvent    记录相关网站事件
|    |            |
|    |            |__ gateway    Gateway相关配置
|    |            |     |_ accesscontrol    
|    |            |     |      |_ AccessControlFilter    自定义增强Zuul过滤器，用于权限限制对微服务端的访问
|    |            |     |_ ratelimiting
|    |            |     |      |_ RateLimitingFilter    自定义增强Zuul过滤器，用于限制对微服务端的次数访问
|    |            |     |_ responserewriting
|    |            |            |_ SwaggerBasePathRewritingFilter   Swagger 过滤器，重写微服务 URL
|    |            |
|    |            |
|    |            |__ repository    Spring Data JPA 的CRUD接口，自定义查询在该接口定义。
|    |            |
|    |            |
|    |            |__ security    安全相关
|    |            |     |
|    |            |     |_ oauth2
|    |            |     |     |_ CookieCollection    操作 Cookie 
|    |            |     |     |_ CookiesHttpServletRequestWrapper    获取进入 Controller 层 HttpServletRequest 的 Cookie 
|    |            |     |     |_ CookieTokenExtractor    从 Cookie 中提取 accessToken 
|    |            |     |     |_ OAuth2AuthenticationService    用户登录获取 token 并刷新 token，在 token 是失效后清除 cookie，或在未失效前重新生成有效的 token
|    |            |     |     |_ OAuth2CookieHelper    oauth2 cookie 操作
|    |            |     |     |_ OAuth2Cookies    鉴权成功后，存储 token 到 cookie
|    |            |     |     |_ OAuth2SignatureVerifierClient    oauth2 鉴权客户端
|    |            |     |     |_ OAuth2TokenEndpointClient    从 uaa 获取、刷新 token 客户端
|    |            |     |     |_ OAuth2TokenEndpointClientAdapter    适配器，实现从 uaa 获取 token 
|    |            |     |     |_ UaaSignatureVerifierClient    从 uaa 获取公钥验证签名是否正确
|    |            |     |     |_ UaaTokenEndpointClient    授权 token 权限 
|    |            |     |
|    |            |     |_ AuthoritiesConstants    用户权限的常量设置
|    |            |     |
|    |            |     |_ ManagerConstants    BackendManae 调用 GatewayUi ，GatewayUi 调用其他 Service 公开接口的 Key 和 Secret
|    |            |     |
|    |            |     |_ SecurityUtils    Securrity 工具类，提供获取当前用户的 principal、用户是否登录、当前用户角色
|    |            |     |
|    |            |     |_ SpringSecurityAuditorAware
|    |            |     
|    |            |2.模块组要功能
|    |            |__ service    业务逻辑类
|    |            |     |
|    |            |     |_ captcha
|    |            |     |    |_ geetest   Geetest 验证
|    |            |     |    |_ CaptchaService   图形验证码
|    |            |     |
|    |            |     |_ email    邮件模板服务
|    |            |     |    |_ MailService    根据 emailType 发送不同的邮件
|    |            |     |    
|    |            |     |_ kyc 
|    |            |     |    |_ ALiYunService    阿里云 OCR 服务
|    |            |     |    |_ KycVerification    KYC 认证状态，根据配置文件级别的国家代码审核
|    |            |     |    |_ KycVerificationChina    当用户国家为 86 时，调用阿里云 OCR 服务
|    |            |     |    |_ KycVerificationService    KYC 服务
|    |            |     |       
|    |            |     |_ multi.thread    多线程
|    |            |     |        |_ ALiYunOssMultiThread   阿里云 oss 文件分片多线程
|    |            |     |        |_ ALiYunOssUploadService    阿里云 oss 文件分片多线程上传（0.5M 一片）
|    |            |     |        |_ AwsOssService            亚马逊 s3
|    |            |     |        |_ OssService       OSS 抽象类，根据配置文件 type 值决定使用哪一种服务
|    |            |     |   
|    |            |     |_ rate 
|    |            |     |    |_ CoinMarketCapLoaderService
|    |            |     |    |_ CoinMarketCapService    获取实时汇率，每三分钟获取一次，并更新数据
|    |            |     |
|    |            |     |_ sms 
|    |            |     |    |_ MultiSMS     SMS 父类    
|    |            |     |    |_ ALiYunSMS    阿里云短信发送（当用户手机号 +86 开头，自动调用）（前提 config 必须配置+86）
|    |            |     |    |_ NexmoSMS    国外短信服务商
|    |            |     |    |_ TwilioSMS    国外短信服务商（当用户不是 +86 时，获取该实例。）
|    |            |     |    |_ SendSmsService    短信服务，此处获取实例
|    |            |     |     
|    |            |     |_ MapiAccountService    创建底层账户    
|    |            |
|    |            |__ web  API 接口
|    |                  |_ filter  
|    |                  |    |_ decode
|    |                  |    |  |_ ChangePassFilter    密码相关的 Base64 解密，因为复杂暂时不适用，直接在 UAA 解密。
|    |                  |    |
|    |                  |    |_ manager
|    |                  |    |  |_ ManagerFilter  backendManage 调用 GatewayUi 公开接口的解析 Filter
|    |                  |    |
|    |                  |    |_ uaa 
|    |                  |    |  |_ ActivateUserPostFilter  Link 方式激活账户使用该 Filter，在用户激活成功后自动创建底层账户，并发送邮件
|    |                  |    |  |_ CreateUserPostFilter    Key 方式注册自动创建底层账户，并发送注册成功邮件。
|    |                  |    |  |_ PreFilter    过滤 /auth/user 的 uri ，转发到 uaa 
|    |                  |    |  |_ RecordIPPostFilter    用户登录后，获取用户 IP 并记录
|    |                  |    |  
|    |                  |    |_ RefreshTokenFilter    过滤访问请求，在 token 过期前刷新并更新
|    |                  |    |_ RefreshTokenFilterConfigurer    refreshToken 刷新配置
|    |                  |  
|    |                  |_ rest    API 接口      
|    |                  |   |_ errors    API异常
|    |                  |   |_ util    工具包
|    |                  |       |_ ALiYunAppHttpUtil    阿里云 API HttpUtil 调用专用工具   
|    |                  |       |_ CryptoHttpEntityUtil    调用加密接口封装 HttpEntity 工具类
|    |                  |       |_ DeviceUtil    获取登录设备工具类
|    |                  |       |_ GoogleAuthenticatorUtil    TOTP 算法，生产 GA 秘钥、验证秘钥
|    |                  |       |_ HeaderUtil    封装 HttpHeader 工具类
|    |                  |       |_ HttpEntityUtil    restTemplate 调用其他模块，使用 exchange 加入鉴权、传输数据工具类
|    |                  |       |_ ImgPath2Base64Util    图片编解码 base64 工具
|    |                  |       |_ IPUtil    获取 IP 地址工具（查询地址后期配置抽离）
|    |                  |       |_ PaginationUtil    分页工具
|    |                  |       |_ QRCodeUtil    二维码工具
|    |                  |       |_ RandomUtil    random 工具
|    |                  |       |_ RedisUtil     Redis 获取自增、设置自增失效时间工具类
|    |                  |       |_ StringConvertUtil    String  工具，目前主要处理 img 、url 路径问题 
|    |                  |       |_ SunBase64Util    Base64 加解密工具类
|    |                  |
|    |                  |
|    |                  |_ vm    数据视图模型
|    |                  |   |_ ip.vm    ip 数据视图
|    |                  |   |_ kyc.vm    kyc C1、C2、C3数据视图、OSS 数据视图
|    |                  |   |_ mapi.vm    底层账户数据视图
|    |                  |   |_ rate.vm    数字币汇率数据视图
|    |                  |   |_ response.vm    携带 code 返回视图（暂未用）
|    |                  |   |_ uaa.vm    uaa 模块数据视图
|    |                  |
|    |                  |
|    |                  |_ AuthResource    用户注册、登录、更新、获取权限后登录(记录 IP)、用户信息、更改密码等
|    |                  |_ GatewayResource    
|    |                  |_ KycResource    KYC 用户 KYC C1、C2、C3 认证校验、重新认证、认证状态、
|    |                  |_ LogsResource    
|    |                  |_ ProfileInfoResource
|    |                  |_ PublicInfoVerifyResource    短信、邮件、图形验证码发送、验证 
|    |                  |_ SecurityBindResource    用户绑定信息、GA 绑定、更新、验证、移除，安全资金密码设置、更新、验证、输入频率设置、频率状态
|    |            
|    |-- resources    资源包
|    |      |_ config    配置文件
|    |      |    |_ liquibase
|    |      |    |      |_ changelog
|    |      |    |      |_ 000000000000_initial_schema.xml    项目初始文件   
|    |      |    |_ bootstrap.yml     根配置文件 
|    |      | 
|    |      |_ i18n   国际化配置文件                       
|    |      |_ mails    邮件发送 html 模板
|    |      |_ templates    error.html 模板
|    |      |_ banner.txt    项目启动 banner
|    |
|    |-- webapp    Gateway 页面
|           |_ app
|               |_ account
|               |_ admin
|               |_ blocks
|               |_ components
|               |_ entities
|               |_ home
|               |_ layouts    
|               |_ services    路径大多在此处更改
|    
|    
|____ pom.xml     maven 项目配置
```

##### 2.模块主要功能

1. AuthResource  实现了用户登录、注销。
2. KycResource  实现了用户 KYC 身份认证。
   1. C1认证：用户国家为中国时，调用阿里云第三方 API 校验用户输入的身份证、驾驶证号。护照因暂时没有 API ，和其他国家一并默认校验通过，获取相关重要数据转发到 UAA 存储到数据库。
   2. C2认证：用户国家为中国时，调用阿里云自有 API 上传到 OSS，并获取 OSS url 进行 （apache）base64 编码，调用阿里云 OCR API 进行扫描中国用户身份证、驾驶证、护照正、反面照片，获取相关重要数据转发到 UAA 存储到数据库。
   3. C3认证：暂时只有用户提交，后台人工审核。后期加入生物识别。
   4. 认证状态：获取用户最高级别认证状态、真实姓名、国家、证件号码、证件类型。C2认证时，必须保持和 C1证件类型一样。
3. PublicInfoVerifyResource  实现了公共信息验证功能。**权限全部开放**
   1. 短信发送、校验
   2. 邮件发送、校验
   3. 图形验证码显示、校验
4. SecurityBindResource  实现了安全信息绑定、校验功能。
   1. 查询用户绑定信息，根据获取的绑定信息，判断用户登录逻辑、验证逻辑、等。
   2. 绑定、重置、移除用户 GA 秘钥、获取用户 GA 秘钥等信息、显示、校验 GA 二维码。**（移除用户 GA 会自动移除资金全密码，因为只有绑定 GA 才可以使用资金安全密码。）**
   3. 设置、修改、校验安全资金密码、设置、获取用户输入安全资金密码输入频率

---

##### 3.  项目启动

1. Gateway 因为有前端页面，在启动空白页时：
   1. yarn install     
      1. 如果安装到第5步，出现卡在 phantomjs-2.1.1-macosx.zip 时，使用迅雷下载，拷贝到提示的对应目录中。（该目录z在同一台电脑中路径不变。）
      2. 如果提示 yarn 版本不对，修改项目根目录的 **.yo-rc.json **yarn 版本号为本地版本号就行。
   2. yarn start 启动前端项目
   3. ./mvnw  启动后端项目，默认启动 pom.xml 文件配置的环境。一般为 dev 环境。
      1. yarn start 一次，在页面不修改的前提下，不需要再单独启动前端项目。因为首次启动，已经编译到 **target **文件内。
      2. 启动别的环境执行 **./mvnw -Pdev   ./mvnw -Pprod  ./mvnw -Ptest**

---

##### 4.项目打包

1. mvn clean package -DskipTests=true -Pdev

2. mvn clean package -DskipTests=true -Pprod

3. mvn clean package -DskipTests=true -Ptest

4. 以上三个命令，自动打包前端页面。

---



