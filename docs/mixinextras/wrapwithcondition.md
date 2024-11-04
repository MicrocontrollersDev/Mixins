# WrapWithCondition

!!! info
    For a more in-depth explanation, see the [MixinExtra's Wiki](https://github.com/LlamaLad7/MixinExtras/wiki/WrapWithCondition).

`WrapWithCondition` lets you wrap a method call with a condition. This is a much simpler and compatible way compared to using a `Redirect` and no-op'ing when a condition fails.

`WrapWithCondition` should be used in favor of `Redirect` when applicable.

Say we had the following code:

```java
public void foo() {
    doSomething();
}
```

Let's say we only wanted to call doSomething when one of our mod's config option is enabled. We could do that as such:

```java
@WrapWithCondition(method = "foo", at = @At(value = "INVOKE", target = "doSomething()V"))
private boolean shouldDoSomething() {
    return ModConfig.configOption;
}
```

This produces:

```java
public void foo() {
    if (ModConfig.configOption) {
        doSomething();
    }
}
```
