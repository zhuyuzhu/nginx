# nginx

简单的实例：https://juejin.cn/post/6901525873531633671

https://juejin.cn/post/6844904129987526663

https://zhuanlan.zhihu.com/p/31202053

https://zhuanlan.zhihu.com/p/130819099

知乎高赞：https://zhuanlan.zhihu.com/p/34943332

首次使用nginx遇到的问题：https://zhuanlan.zhihu.com/p/107216078

nginx跨域问题：https://zhuanlan.zhihu.com/p/94197713



### 官网

中文文档：https://www.nginx.cn/doc/index.html

英文文档：http://nginx.org/en/download.html

## nginx

Nginx是一款**轻量级的Web服务器**、**反向代理服务器**，由于它的内存占用少，启动极快，**高并发**能力强，在互联网项目中广泛应用。

#### 反向代理

**正向代理：**代理代表的是客户端，代理去访问目标服务器，获取资源。

比如：VPN

![img](https://user-gold-cdn.xitu.io/2020/4/17/171864e773f05fe7?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

VPN的原理：多个客户端访问VPN服务器，由VPN服务器去访问目标Server服务器。此时VPN服务器代表了客户端。



**反向代理：**代理代表服务器，客户端们来访问该服务器。该服务器再去实际服务器中获取资源。

比如：现实中的代购、负载均衡、跨域。

![img](https://user-gold-cdn.xitu.io/2020/4/16/17183720f7a66978?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

>  nginx 就是充当图中的 proxy。左边的3个 client 在请求时向 nginx 获取内容，是感受不到3台 server 存在的。此时，proxy就充当了3个 server 的反向代理。(服务器可以有一个或多个)

##### 反向代理的作用

1. 保障应用服务器的安全（增加一层代理，可以屏蔽危险攻击，更方便的控制权限）
2. 实现负载均衡（稍等~下面会讲）
3. 实现跨域（号称是最简单的跨域方式）



### 负载均衡

随着业务的不断增长和用户的不断增多，一台服务已经满足不了系统要求了。这个时候就出现了服务器 [集群](https://www.cnblogs.com/bhlsheji/p/4026296.html)。

在服务器集群中，Nginx 可以将接收到的客户端请求“均匀地”（严格讲并不一定均匀，可以通过设置权重）分配到这个集群中所有的服务器上。这个就叫做**负载均衡**。

##### 负载均衡的作用

- 分摊服务器集群压力
- 保证客户端访问的稳定性

Nginx还带有**健康检查**（服务器心跳检查）功能，会定期轮询向集群里的所有服务器发送健康检查请求，来检查集群中是否有服务器处于异常状态。

一旦发现某台服务器异常，那么在这以后代理进来的客户端请求都不会被发送到该服务器上（直健康检查发现该服务器已恢复正常），从而保证客户端访问的稳定性。

### 动静分离

这样做不仅能给应用服务器减轻压力，将后台api接口服务化，还能将前后端代码分开并行开发和部署。

nginx动静分离的好处：https://www.php.cn/nginx/424631.html

![img](https://user-gold-cdn.xitu.io/2020/4/17/171867d175eae45f?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)

### 配置



###  使用



### 其他知识：

入口网关

VPN原理：https://zhuanlan.zhihu.com/p/71534299

VPN（Virtual Private Network）!即虚拟私有网络。VPN用户和VPN服务器之间的通讯是加密的，这样就不会被黑客盗取内容。