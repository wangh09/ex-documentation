### Jmeter Test Guide

---

##### 1.Get the Java Request Code

```
   git clone http://gitlab.ziggurat.cn/ink-assets/jmeter-matching-test.git
   or git clone https://github.com/suguiyun/jmeter-performance-test.git
```

##### 2.Structure

```
|-- src
|    |-- main/java
|    |     |_ com.cryproex     
|    |            |
|    |            |
|    |            |__ errors    
|    |            |     |_ BadRequestException    异常返回封装类
|    |            |
|    |            |__ response
|    |            |     |_ BusinessOrder    订单返回封装类
|    |            |
|    |            |
|    |            |__ utils    工具类
|    |            |     |_ ByteUtil    字节处理工具
|    |            |     |_ HashUtil    HASH算法工具
|    |            |     |_ JsonUtil    JSON工具
|    |            |
|    |            |
|    |            |__ Client    远程调用客户端
|    |            |__ JmeterPerformanceTest   The main class Jmeter测试调用方法
|    |            |__ JsonKey    获取json文件封装类
|    |            
|    |-- resources    资源包
|           |_ init-keys.json    API-KEYS 初始化API文件
```

##### 3.Deployment

```
（1）Package the jar，and put the jar to "jmeter home"/lib/ext
（2）start Jmeter（open "jmeter home"/bin/jmeter）
（3）Create test plan
```

![](/assets/createThreads.png)

（4）Create java request

![](/assets/CreateJavaRequest.png)![](/assets/CreateJavaRequest%282%29.png)

```
It should be pointed out that, the inNum is used to pick different API-keys for different thread(user).
```

（5）Save the test plan, and upload it to the test server

\(6\) run it on the test server

bin/jmeter -n -t jmeterPT.jmx -l test.jtl

bin/jmeter -g test.jtl -o test

