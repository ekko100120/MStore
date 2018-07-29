---
title: java内存模型
date: 2018-07-29 10:12:48
tags: Java cache 分布式

---
***
## java Cache
***

#### 常见CacheAPI
* 单JVMcache：guava cache，Hibernate EHCache,spring cache




[https://segmentfault.com/a/1190000007608782](https://segmentfault.com/a/1190000007608782)

### 一致性hash算法

##### 1 背景
>一致性hash作为一个负载均衡算法，可以用在分布式缓存、数据库的分库分表等场景中，还可以应用在负载均衡器中作为作为负载均衡算法。在有多台服务器时，对于某个请求资源通过hash算法，映射到某一个台服务器，当增加或减少一台服务器时，可能会改变这些资源对应的hash值，这样可能导致一部分缓存或数据失效了。一致性hash就是尽可能在将同一个资源请求路由到同一台服务器中

##### 2.解决的问题

> 一致性hash以及普通hash在增加、删除节点之后，对数据分布、缓存命中率的

#### Reference
![一致性hash原理](pic/一致性hash原理.png)

[http://www.zsythink.net/archives/1182](http://www.zsythink.net/archives/1182)
