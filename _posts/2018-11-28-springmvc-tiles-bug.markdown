---
layout: post
title:  "SpringMVC Cannot Intercept ROOT Request"
date:   2018-11-28 18:00:00 +0800
categories: 
---

In a Spring MVC + Apache Tiles project, where the URI for home page is `/home`, I tried to redirect the requests for `/` and `index` to the home page.

```
    @GetMapping(value = "/")
    public String indexPageDefault() {
        return "redirect:/home";
    }

    @GetMapping(value = "/index")
    public String indexPageWithFileName() {
        return "redirect:/home";
    }
```

It turned out the `/index` could be redirected to `/home` and `/home` could be displayed, but `/` is never intercepted because the controller for `/`, that is, `indexPageDefault()` is never called.

It turned out this is an internal bug of Spring MVC + Tiles as in [this thread](http://forum.spring.io/forum/spring-projects/web/94732-requestmapping-on-root-url-bug). I made the same attempt as the OP, adding an wildcard after `/` in the servlet mapping configuration in `web.xml`:

```
    <servlet-mapping>
        <servlet-name>VineWebPages</servlet-name>
        <url-pattern>/*</url-pattern>
    </servlet-mapping>
```

This is a bad practice because:
- this is not what I want;
- and it crashed everything. All requests resulted in `404` with this wildcard.

If you insist on redirecting `/` to your home page, **an workaround would be configure an proxy in Nginx while deploying your project**.


References:

- [@REQUESTMAPPING ON ROOT "/" URL BUG?](http://forum.spring.io/forum/spring-projects/web/94732-requestmapping-on-root-url-bug)