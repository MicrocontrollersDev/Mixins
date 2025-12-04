# Method

The most important part for most injectors is our method. We need to tell Mixin what method we are trying to inject into.

As you'll see in most pages in this guide, we can simply declare the method we are targetting in the injector itself. For example,

```java
@Inject(method = "foo", at = ...)
```

Simple!

If we wanted to inject the same code across multiple methods, we can also do so quite easily. The method argument can take an array as well. For example,

```java
@Inject(method = {"foo", "bar"}, at = ...)
```

This can allow for a lot of code deduplication *if used correctly*. Do be careful when modifying many methods at once, this is usually only useful for something such as canceling at head or similar.
