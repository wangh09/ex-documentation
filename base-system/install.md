# 安装JDK 8

可安装Oracle JDK 8或Open JDK 8。

注意：安装完成后必须从Oracle网站下载JCE Unlimited Policy：
http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html

并按照相关文档覆盖JDK的policy文件，否则在使用256位加密时会报Illegal Key Size错误。

# 安装Maven

安装Maven 3.x，推荐使用Aliyun镜像加速：

配置文件：`~/.m2/settings.xml`

``` 
<settings>
  <mirrors>
    <mirror>
      <id>aliyun</id>
      <name>aliyun</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <mirrorOf>central</mirrorOf>
    </mirror>
  </mirrors>
</settings>
```

# 安装Node

安装Node >= 8.x

```
$ node -v
v8.1.4
$ npm -v
5.0.3
```

# 安装MySQL数据库

开发环境建议设置root口令为password，可以直接运行初始化脚本；

执行CryptoApiSchemaBuilder，输出ex.sql和init-ex.sql，执行：

```
mysql -u root --password=password < path/to/ex.sql
mysql -u root --password=password < path/to/init-ex.sql
```

执行CryptoUISchemaBuilder，输出ui.sql，执行：

```
mysql -u root --password=password < path/to/ui.sql
```

执行CryptoManageSchemaBuilder，输出mg.sql和init-mg.sql，执行：

```
mysql -u root --password=password < path/to/mg.sql
mysql -u root --password=password < path/to/mg-init.sql
```

# 安装Rocket MQ

安装Rocket MQ 4.2，启动namesrv和mq请参考：https://rocketmq.apache.org/docs/quick-start/

可以保持Rocket MQ后台运行。

# 安装Redis

安装Redis 3.x

# 编译

进入build目录，执行：

`mvn -DskipTests clean package`

执行成功后，会打包如下文件：

* api/target/crypto-api.jar
* config/target/crypto-config.jar
* manage/target/crypto-manage.jar
* match/target/crypto-match.jar
* sequence/target/crypto-sequence.jar
* ui/target/crypto-ui.jar

必须先启动Config Server：

```
config$ java -jar target/crypto-config.jar
```

然后，分别启动api/manage/match/sequence/ui（无特定顺序），启动方式均为`java -jar xxx.jar`

端口配置参见config-files，默认端口在本地启动不冲突。

UI启动成功后，可以访问首页：http://localhost:8080

并注册、登录。

Manage启动成功后，可以访问：http://localhost:8008

各组件启动成功后，不再依赖config服务。即仅需在启动时保证config server可用。

## 启动WebSocket行情

进入notification目录，安装依赖包，执行：

```
npm install
```

成功后，执行`node loader.js`

WebSocket服务将在3000端口运行。进入UI行情页，所有行情均由WebSocket推送。

# 清除数据

开发阶段需要清除数据时：

1. 停止ex所有组件；
2. 停止RocketMQ；
3. 运行初始化脚本，将删除数据库并重新创建
4. 删除RocketMQ的logs和store文件夹
5. 删除撮合快照/var/match-engine-snapshot

特别注意：如果没有执行4，将导致消息顺序混乱，如果没有执行5，将导致撮合获得错误的历史数据。
