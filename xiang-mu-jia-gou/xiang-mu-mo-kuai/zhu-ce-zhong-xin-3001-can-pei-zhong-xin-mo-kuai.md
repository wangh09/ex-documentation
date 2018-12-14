### 注册中心、参配中心 ink-registry 模块

---

##### 1.**注册中心**

1. 所有模块通过 `model-name.yml`** 应用名字\[ 唯一标识 \] **注册到注册中心。
   ```
   spring:
       application:
           name:
   ```

---

##### 2.参配中心

1. ink-registry 项目 `resources 目录，config 包路径下 bootstap.yml 文件`

   1. 具体根据环境配置，使用对称加解密

      1. uri 配置 git 路径，只搜索该 git 下的 search-paths

      2. username 配置用户名

      3. password 配置密码

      4. search-paths 指定搜索路径，如果有多个路径则使用 , 分隔

   2. 1. ```
         spring:
             application:
                 name: ink-registry
             profiles:
                 active: dev
             cloud:
                 config:
                     server:
                         git:
                             uri: http://gitlab.ziggurat.cn/gongtao/test-ink-ex-config.git # 配置 git 路径
                             username: '{cipher}c5bd9b0b140bb288f3a9bad8f017e548aee4a6958c3445bb97daaebe0a7bf422614a47e3a66225745c83baf9011b04a6'
                             password: '{cipher}8a5724e7afd635a044a10aca04eabf0dd46d0ef4a5ca7bc5ad0b6ed847d2aaa5'
                             search-paths:
         ```

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



