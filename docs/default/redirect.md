# Redirect

!!! warning
    `Redirect`s are not recommended as they cause hard conflicts with any other mod attempting to mixin into the same location. They can usually be replaced by either a [`WrapOperation`](https://mixins.microcontrollers.dev/mixinextras/wrapoperation) or [`WrapWithCondition`](https://mixins.microcontrollers.dev/mixinextras/wrapwithcondition)

`Redirect` lets you redirect a method call to a different method. Additionally, we can also 

Say we had the following:

```java
public void foo(int param) {
    int a = getInt(param);
    String b = getString(param);
    boolean c = getBool(param);
    doSomething(a, b, c);
}
```

If we want to change the doSomething to something else, wrap the original call in a check, or simply skip the call altogether, we can do that as such.

```java
@Redirect(method = "foo", at = @At(value = "INVOKE", target = "doSomething(ILjava/lang/String;Z)V"))
private void wrapSomething(Foo instance, int a, String b, boolean c, Operation<Void> original) {
    if (ModConfig.doSomethingElse) {
        return doSomethingElse(a, b, c);
    } else if (ModConfig.doOriginal) {
        return doSomething(a, b, c);
    } else {
        // No-op (the original method call is skipped entirely)
    }
}
```

Resulting in:

```java
public void foo(int param) {
    int a = getInt(param);
    String b = getString(param);
    boolean c = getBool(param);
    if (ModConfig.doSomethingElse) {
        doSomethingElse(a, b, c);
    } else if (ModConfig.doOriginal) {
        doSomething(a, b, c);
    } else {
        // No-op
    }
}
```

However, we can replace this `Redirect` with other injections for better comptability.

* If we want to replace the original call, we should use [`WrapOperation`](https://mixins.microcontrollers.dev/mixinextras/wrapoperation).
* If we just want to wrap the original call with a check, we should use [`WrapWithCondition`](https://mixins.microcontrollers.dev/mixinextras/wrapwithcondition).
