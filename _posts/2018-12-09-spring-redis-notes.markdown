---
layout: post
title:  "Some Notes on Using SpringFramework RedisTemplate"
date:   2018-12-09 10:30:00 +0800
categories: 
---

I got two tricky problems while importing and using Spring RedisTemplate with Maven, which took me hours to solve. Hope this post save your time if you have the same problem.

### java.lang.NoSuchMethodError

I got almost exactly the same error as posted in [this question](https://stackoverflow.com/questions/50944891/spring-data-redis-java-lang-nosuchmethoderror-org-springframework-util-assert-i). It is easy to solve: either you upgrade Spring jars to be over 5.x if you want to use Spring Redis 2.x, or you keep Spring jars of version under 5.x but use Spring Redis under 2.x instead. I opted for the latter.

But it is interesting to inspect the error. The error says
`Spring data redis java.lang.NoSuchMethodError: org.springframework.util.Assert.isTrue(ZLjava/util/function/Supplier;)`

Basically it is telling us that, while the Spring Redis is looking for a method in the Spring jars, it could be find a method that is supposed to be there.

### Cannot Set <Key, Value> Pairs to Redis with RedisTemplate

I was able to `@Autowired` a RedisTemplate and print it out, which means the basic configuration was fine, but I just could not set any data into Redis. This kind of problems is annoying because it throwed no error or exception.

#### Redis Server

A possible culprit could be that the Redis server has not been started. Type `redis-server [config-file-path]` and things would probably work.

#### Serialization

In my case, the problem lay in the serialization of my keys and values. I took it for granted that Spring would do all the serialization stuff for me (otherwise why I would pick Spring, LOL), but before automation configuration must be done.

In the Spring Redis configuration part in the `applicationContext.xml` file(your file might have a different name), do add the serialization beans for both keys and values:

```
<bean>
	...

    <bean id="stringSerializer" class="org.springframework.data.redis.serializer.StringRedisSerializer"/>
    <bean id="objectSerializer" class="org.springframework.data.redis.serializer.GenericJackson2JsonRedisSerializer"/>

    <bean id="redisTemplate" class="org.springframework.data.redis.core.RedisTemplate">
        <property name="connectionFactory" ref="connectionFactory"/>
        <property name="keySerializer" ref="stringSerializer"/>
        <property name="valueSerializer" ref="objectSerializer"/>
        <property name="hashKeySerializer" ref="stringSerializer"/>
        <property name="hashValueSerializer" ref="objectSerializer"/>
        <!-- 开启事务，可以通过transcational注解控制 -->
        <property name="enableTransactionSupport" value="true"/>
	</bean>
	...

</beans>
```

The serialization class pair for both normal `set` and `hmset` is the same.

References:

[Spring data redis java.lang.NoSuchMethodError: org.springframework.util.Assert.isTrue(ZLjava/util/function/Supplier;)V](https://stackoverflow.com/questions/50944891/spring-data-redis-java-lang-nosuchmethoderror-org-springframework-util-assert-i)
