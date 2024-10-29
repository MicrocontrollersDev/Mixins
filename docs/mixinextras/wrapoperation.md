# WrapOperation

For a more in-depth explanation, see the [MixinExtra's Wiki](https://github.com/LlamaLad7/MixinExtras/wiki/WrapOperation).

Similar to `Redirect`s, `WrapOperation` lets you replace a method call with your own. However, unlike `Redirect`s, they will stack when several mods attempt to inject into the same one.

Use `WrapOperation` instead of `Redirect` when applicable.

Say we have the following code:

```java
public void foo(int param) {
    int a = getInt(param);
    String b = getString(param);
    boolean c = getBool(param);
    doSomething(a, b, c);
}
```

Instead of using a redirect, we can wrap the operation as such:

```java
@WrapOperation(method = "foo", at = @At(value = "INVOKE", target = "doSomething(ILjava/lang/String;Z)V"))
private void wrapSomething(Foo instance, int a, String b, boolean c, Operation<Void> original) {
    if (ModConfig.replace) {
        return doSomethingElse(a, b, c);
    } else {
        return original.call(instance, a, b, c); // we can call the original method using original.call instead of actually calling the method itself
    }
}
```

This will produce:

```java
public void foo(int param) {
    int a = this.getInt(param);
    String b = this.getString(param);
    boolean c = this.getBool(param);
    if (ModConfig.configOption) {
        doSomethingElse(a, b, c);
    } else {
        doSomething(a, b, c);
    }
}
```
