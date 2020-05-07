---
title: ThreadLocal在项目中的使用与延伸
categories: 
    - java基础
tags: 
    - ThreadLocal
---

### 背景

对于java web开发者而言，经常需要当前登录的用户信息。而如何高效快速的获取当前登录用户的信息，业界都有多种解决方案。本次将介绍如何使用 ```ThreadLocal``` 来解决


### 案例

#### 思路
* 用户登录后将登录信息放到redis中 同时会返回一个访问用户的accessToken
* 在web 拦截器中 可以根据 accessToken 获取用户信息
* 将登录的用户信息放到 ThreadLocal 中

```java

/*
 * @author <a href="mailto:hbsy_zhb@163.com">zhangbin</a>
 */
@Slf4j
@Component
public class PortalHandlerInterceptor extends HandlerInterceptorAdapter {

    @Resource
    private RedisTemplate<String, LoginInfo> redisTemplate;

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        String reqUrl = request.getRequestURI();
        if (StringUtils.isEmpty(reqUrl) || reqUrl.equals("/")) {
            return true;
        }
        // 创建请求上下文的ThreadLocal（在当前线程内）
        ReqContext context = ReqContext.getContext();
        // 从Header 里面获取accessToken
        String accessToken = request.getHeader(PortalConstants.ACCESS_TOKEN);
        if (StringUtils.isEmpty(accessToken)) {
            return true;
        }
        context.setAccessToken(accessToken);
        // 根据 accessToken 获取当前登录用户的信息
        LoginInfo loginInfo = redisTemplate.opsForValue().get(accessToken);
        // 将登录的用户信息放入到ThreadLocal中
        context.setLoginInfo(loginInfo);
        return super.preHandle(request, response, handler);
    }


    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) {
        ReqContext.clear();
    }
}


/**
 * @author <a href="mailto:hbsy_zhb@163.com">zhangbin</a>
 */
@Getter
@Setter
@FieldDefaults(level = AccessLevel.PRIVATE)
public class ReqContext {
    
    private static ThreadLocal<ReqContext> context = ThreadLocal.withInitial(ReqContext::new);

    public static ReqContext getContext() {
        return context.get();
    }

    public static void clear() {
        context.remove();
    }

    String accessToken;

    LoginInfo loginInfo;

    Map<String, ?> attachment;

}

// 在后续的 控制层可以通过如下方式就可以获取用户的基本信息
LoginInfo loginInfo = ReqContext.getContext().getLoginInfo();

```
### 浅析
通过阅读上面的代码和注释，相信读者对```ThreadLocal```也稍微有点认识了，接下来作者就简单的介绍下它

通过对源码了解```ThreadLocal```可以通过下面两种方式来赋值

``` 
    public static <S> ThreadLocal<S> withInitial(Supplier<? extends S> supplier) {
        return new SuppliedThreadLocal<>(supplier);
    }


    public void set(T value) {
        Thread t = Thread.currentThread();
        ThreadLocalMap map = getMap(t);
        if (map != null)
            map.set(this, value);
        else
            createMap(t, value);
    }
```

