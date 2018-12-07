---
layout: post
title:  "Why Encapsulating Memcached/Redis Client?"
date:   2018-12-07 11:00:00 +0800
categories: 
---

When attempting to incorporate caching service into our projects, there could be two practices:
- Import caching client into our service layer;
- Import caching client into a utility class, encapsulate the client's methods, and use the utility class, rather than directly the client itself, in the service layer.

While the first option seems obviously more straightforward and intuitive, the second one would be safer and more efficient in the future, probably saving a lot of our time. The latter practice also complies with the decoupling principle.

Here's my Memcached utility class that encapsulates SpyMemcached client for illustration(please note the same principle applies to Redis client too, or perhaps any other client that has more than one popular third-party implementations):

```
package com.wszhan.vine.util;

import lombok.extern.log4j.Log4j;
import net.spy.memcached.MemcachedClient;
import java.net.InetSocketAddress;
import java.util.Collection;
import java.util.Map;
import java.util.concurrent.Future;

/**
 * This is an utility class based on the net.spy.memcached.MemcachedClient API:
 * http://dustin.sallings.org/java-memcached-client/apidocs/
 *
 * The class contains static methods and member variables and is to be used
 * without being instantiated.
 *
 * @author Weisi Zhan
 * @create 2018-12-05 16:00
 **/
@Log4j
public class MemcachedUtil
{
    /**
     * Initialization part.
     */
    public static MemcachedClient memcachedClient;
    public static final String HOST = "127.0.0.1";
    public static final int PORT = 11211;

    // Static initialization block is executed
    // when the class is loaded for the first time
    static {
        log.info("Static initialization block running...");

        if (memcachedClient == null) {
            try {
                memcachedClient = new MemcachedClient(
                        new InetSocketAddress(HOST, PORT)
                );
            } catch (Exception e) {
                log.fatal(e.getStackTrace());
            }
        }
    }

    public static MemcachedClient getMemcachedClient()
    {
        return memcachedClient;
    }
    // Empty constructor
    private MemcachedUtil() { }

    /**
     * Encapsulates client methods into methods of this particular utility class
     * for the purpose of decoupling.
     */

    public static Future<Boolean> set(String key, int exp, Object o)
    {
        return memcachedClient.set(key, exp, o);
    }

    public static Object get(String key)
    {
        return memcachedClient.get(key);
    }

    public static Future<Boolean> add(String key, int exp, Object o)
    {
        return memcachedClient.add(key, exp, o);
    }

    public static Future<Boolean> delete(String key)
    {
        return memcachedClient.delete(key);
    }

    public static Future<Boolean> flush()
    {
        return memcachedClient.flush();
    }

    public static void shutdown()
    {
        memcachedClient.shutdown();
    }

    public static Map<String, Object> getBulk(Collection<String> keys)
    {
        return memcachedClient.getBulk(keys);
    }

    public static Map<String, Object> getBulk(String ... keys)
    {
        return memcachedClient.getBulk(keys);
    }

    public static Future<Boolean> replace(String key, int exp, Object o)
    {
        return memcachedClient.replace(key, exp, o);
    }

    /**
     * Unit test to test the static methods.
     * @param args
     */
    public static void main(String[] args)
    {
    	...
    }
}

```

Let's take one method for example:
```
    public static Object get(String key)
    {
        return memcachedClient.get(key);
    }
```

At the first glance, this seems intuitively redundant. Why not just let the utility class return a client and just use the client in the service layer? This works too but it undermines, if any, future upgrading to our application.

Say we use the client for its `set` method everywhere in our code, such as:
```
memcachedClient.set(String key, int exp, Object o);
```
, and one day our team, for some weird but practical reasons, must switch to another client. This doesn't matter unless, unfortunately, the `set` method of the new client requires parameters in this order:
```
memcachedClient.set(String key, Object o, int exp);
```
In this case, we **have to** go through our code **line by line** and replace all legacy codes with this old client with new client methods, not to mention we might use more than one methods of a particular client.

However, **if we encapsulates the client in our utility class, then what we must modify is nothing but less than dozens of lines of code in our utility class**. In the above example, if it is only the `set` method that needs modifications on the parameter order, what we need to do is nothing but to change this line:
```
    public static Future<Boolean> set(String key, int exp, Object o)
    {
        return memcachedClient.set(key, exp, o);
    }
```
to
```
    public static Future<Boolean> set(String key, int exp, Object o)
    {
        return memcachedClient.set(key, o, exp);
    }
```
I bet you might not be able to find out the change at first glance :-)

In summary, if you are try to incorporating functions that would be ubiquitous (not necessarily third-party ones) in your code, it would be wise to construct a utility class that encapsulates the functionalities and, only after then, comfortably add them to your code.

Investing more on the right thing at the very beginning earns you thousands times more in the future.
