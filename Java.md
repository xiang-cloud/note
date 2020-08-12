# Java

### String、StringBuilder、StringBuffer

+ String、StringBuffer是线程安全的，StringBuilder是线程不安全的。

#### 一、替换和删除（replace）

```java
String str = "Hello";str = str.replace("target", "replacement");


```

#### 二、拆分（split）、合并（join）

```java
String s ="boo:and:foo";
// 我们对 s 进行了各种拆分，演示的代码和结果是：
s.split(":")    // 结果:["boo","and","foo"]
s.split(":",2)  // 结果:["boo","and:foo"]
s.split(":",5)  // 结果:["boo","and","foo"]
s.split(":",-2) // 结果:["boo","and","foo"]
s.split("o")    // 结果:["b","",":and:f"]
s.split("o",2)  // 结果:["b","o:and:foo"]

// join的使用，结果为：123,456
String join = str.join(",", "123","456");
```

### stream

```java
Map<Integer, Integer> collect = cartList.stream()
    .filter(e -> e.getProductSelected().equals(false)) //保留List中productSelected属性中为false的
    .map(e -> {
        e.setQuantity(0);
        return e;
    }) // 对List中的对象的进行处理，在这里将两个属性置为0
    .sorted(Comparator.comparing(Cart::getProductId).reversed())  // 根据productId降序排序(Map无效)
    .collect(Collectors.toMap(Cart::getProductId, Cart::getQuantity));// 转为List
```

### 正反序列化

+ 使用gson、fastson、jackson进行序列化

```java

// Gson正反
People people = gson.fromJson(DATA, People.class);
String json = gson.toJson(people1);
// Jackson正反
ObjectMapper mapper = new ObjectMapper();
String s = mapper.writeValueAsString(people1);
People people = mapper.readValue(DATA2, People.class);
// fastjson正反
String jsonString = JSON.toJSONString(people1);
People parseObject = JSON.parseObject(DATA, People.class);
```

### 反射





### MD5摘要算法

> ```java
> String s = DigestUtils.md5DigestAsHex("hello".getBytes(StandardCharsets.UTF_8));
> ```

# Java架构师

> 单体>集群>分布式>微服务 `高可用、高并发、高性能`
> 

## 阶段一：单体电商项目架构，开发与上线（1~5周）

### 第1周 万丈高楼，地基首要

### 第2周 分类，推荐，搜索，评价，购物车开发

### 第3周 地址，订单，支付，定时任务开发

### 第4周 用户中心，订单/评价管理开发

### 第5周 云服务器部署上线

## 阶段二：从单体到高可用集群演进（6~8周）

### 第6周 LVS+Nginx实现高可用集群

### 第7周 主从复制高可用Redis集群

### 第8周 Redis缓存雪崩，穿透

## 阶段三：分布式架构-逐个击破分布式核心问题（9~17周）

### 第9周 分布式会话与单点登录SSO

### 第10周 分布式搜索引擎-ES

### 第11周 分布式文件系统-FastDFS+OSS

### 第12周 分布式消息队列-RabbitMQ

### 第13周 分布式消息队列-Kafka

### 第14周 分布式锁

### 第15周 读写分离、分库分表

### 第16周 分布式全局ID、分布式事务与数据一致

### 第17周 分布式接口幂等性，分布式限流

## 阶段四：基于SpringCloud改造微服务（18~25周）

### 第18周 微服务架构认知、服务治理-Eureka

### 第19周 负载均衡、服务通信与调用

### 第20周 服务容错-Hystrix

### 第21周 分布式配置中心-Config

### 第22周 消息总线、服务网关

### 第23周 服务调用链追踪、消息驱动

### 第24周 微服务下Sentinel

### 第25周 服务治理的另一条出炉-Dubbo

## 阶段五：服务器熔断化-Docker与K8S（26~30周）

### 第26周 服务容器化-Docker

### 第27周 容器技术-Cloud Foundry

### 第28周 容器编排-Messos+Marathon

### 第29周 容器编排-K8S

### 第30周 容器弹性扩缩容

## 阶段六：高性能网络通信-Netty与性能调优（31~40周）

### 第31周 高性能网络通信基石-Netty入门与提高

### 第32周 高性能网络通信基石-Netty最佳实践

### 第33周 基于Netty打造RPC通信框架-1

### 第34周 基于Netty打造RPC通信框架-2

### 第35周 应用监控与调优-工具篇

### 第36周 应用监控与调优-技巧与实战篇

### 第37周 JVM性能调优-理论+工具篇

### 第38周 JVM性能调优-实战篇

### 第39周 数据库监控与调优

### 第40周 Linux调优与架构调优

# Java通用支付实战

## SpringBoot初始化

+ 暂无

## Mybatis三剑客

+ 

### 使用mybatis

```java
@Mapper
public interface CategoryMapper {
    @Select("select * from mall_category where id = #{id}")
    Category findById(@Param("id") Integer id);
}

@RunWith(SpringRunner.class)
@SpringBootTest
public class MallApplicationTests {
    @Autowired
    private CategoryMapper categoryMapper;
    @Test
    public void contextLoads() {
        Category category = categoryMapper.findById(100001);
        System.out.println(category.toString());
    }
}

```

yml文件的配置

```yml
spring:
  datasource:
    url: jdbc:mysql://121.199.70.205:3306/mall?characterEncoding=utf-8&useSSL=false
    driver-class-name: com.mysql.cj.jdbc.Driver
    username: root
    password: ******
# 使得实体类中parentId对应parent_id
mybatis:
  configuration:
    map-underscore-to-camel-case: true
```

### Mybatis-generator

```shell
mvn mybatis-generator:generate
```



## 支付

### 支付场景

> 微信文档： https://pay.weixin.qq.com/wiki/doc/api/index.html 
>
> 支付宝文档：  https://openhome.alipay.com/docCenter/docCenter.html

#### 微信支付方式及支付宝支付

+ 付款码支付（超市收银员扫描手机上的支付码）

+ JSAPI支付（公众号上面点击之后触发的支付、使用链接就可以支付）  ps：不用关注公众号。
+ Native支付（打开微信扫描二维码支付）
+ App支付（就是App集成微信支付，比如说QQ阅读点击付款之后跳出微信支付
+ H5支付（在微信客户端以外的地方唤醒微信支付，从外部浏览器唤醒微信支付）
+ 小程序支付（在小程序中唤醒的支付）

| 对比栏目           | JSAPI                                                        | JSSDK       | 小程序                          |
| ------------------ | ------------------------------------------------------------ | ----------- | ------------------------------- |
| 统一下单           | 都需要先获取到Openid，调用相同的API                          | 同          | 同                              |
| 调起数据签名       | 五个字段参与签名(区分大小写)：appId,nonceStr,package,signType,timeStamp | 同          | 同                              |
| 调起支付页面协议   | HTTP或HTTPS                                                  | HTTP或HTTPS | HTTPS                           |
| 支付目录（白名单） | 有                                                           | 有          | 无                              |
| 授权域名           | 有                                                           | 有          | 无                              |
| 回调函数           | 有                                                           | success回调 | complete、fail、success回调函数 |

+ 人脸支付

微信和支付宝的对比

| 微信支付方式 | 支付宝支付方式               |
| ------------ | ---------------------------- |
| 付款码支付   |                              |
| JSAPI支付    |                              |
| Native支付   | 扫码支付                     |
| App支付      | App支付                      |
| H5支付       | 手机网站支付（电脑网站支付） |
| 小程序支付   |                              |
| 人脸支付     | 刷脸付                       |

### 同步异步

+ 打电话算是同步（能立即得到回应）

+ 发短信算是异步（不能立刻得到回应）
  + 转账算是异步

### 支付系统

+ 独立的系统
+ 独立的数据库/表

## 支付系统架构

### null

### 微信支付异步通知

### 支付宝密钥

+  应用公私密钥
+ RSA非对称加密
  + 发起支付：支付系统（应用私钥）->支付宝（应用公钥）
  + 异步通知：支付宝（支付宝私钥）->支付系统（支付宝公钥）
+ RSA签名不等于RSA加密
+ 一般加解密使用AES加密

## 小技巧

### 读取yml文件中的配置

+ yml文件中进行如下配置：

```yml
wx:
  appId: wxd898fcb01713c658
  mchId: 1483469312
  mchKey: 098F6BCD4621D373CADE4E832627B4F6
  notifyUrl: http://undefined-gx.natapp1.cc/pay/notify
  returnUrl: http://127.0.0.1
```

+ java文件中配置如下所示，调用这个实体类就可以获取配置



```java
@Component
@ConfigurationProperties(prefix = "wx")
@Data
public class WxAccountConfig {
    private String appId;
    private String mchId;
    private String mchKey;
    private String notifyUrl;
    private String returnUrl;
}
```

## 用户模块设计

### Service注册模块设计与测试



### Controller接收参数

+ String方式

```java
@PostMapping("register")// 有了RequestParam之后参数名字可以随便起
public void register(@RequestParam(value = "username") String username){ 
	log.info("username={}", username);
}
```

+ Obejct方式

```java
@PostMapping("register")
public void register(User user){ //传递的参数必须和Object中的属性相同 
	log.info("username={}", username);
}

@PostMapping("register") //传递数据类型为json时必须加上RequestBody
public void register(@RequestBody User user){ //传递的参数必须和Object中的属性相同 
	log.info("username={}", username);
}
```

### 表单的验证



### 实战登陆



### Cookie、Session

+ 使用sessionId存入到浏览器的cookie中
+ 升级版是使用token和redis配合

Cookie 跨域

+ 登录状态什么时候消失？

  过期的时候、服务重启、浏览器重启。

 ### 拦截器模块的开发

+ Interceptor----Url

```java
@Slf4j  // 1、实现接口 2、重写默认方法 
public class UserLoginInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        log.info("preHandle...");
        User user = (User) request.getSession().getAttribute(MallConst.CURRENT_USER);
        if (user == null) {
            log.info("user==null");
            throw new UserLoginException();
        }
        return true;
    }
}

@Configuration  // 1、实现接口 2、重写默认方法 3、注解
public class InterceptorConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new UserLoginInterceptor())
                .addPathPatterns("/**")
                .excludePathPatterns("/user/login", "/user/register");
    }
}
```

+ AOP ----包名

### 单元测试

> mvn clean package -Dmaven.test.skip=true