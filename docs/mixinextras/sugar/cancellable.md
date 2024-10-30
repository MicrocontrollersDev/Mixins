# Cancellable

`Cancellable` lets you use CallbackInfo or CallbackInfoReturnable on any type of injection.

We can use `Cancellable` by adding either of the following to the mixin method arguments:
* `@Cancellable CallbackInfo ci` for a void method
* `@Cancellable CallbackInfoReturnable<ReturnType> cir` for a non-void method

Say we had the following code:

```java
public void foo(int p) {
    int a = doSomething(p);
    int b = doSomething(p);
    doSomethingTwo(a + b); 
}
```

If we wanted to ModifyArgs the first doSomething, and potentially early return after it, we could do so with `Cancellable`:

```java
@ModifyArgs(method = "foo", at = @At(value = "INVOKE", target = "doSomething(I)I"), ordinal = 0)
private void doSomethingElse(Args args, @Cancellable CallbackInfo ci) {
    int ret = (int) args.get(1) + 1
    args.set(0, ret);
    if (ret > 5) {
        ci.cancel();
    }
}
```

This results in:

```java
public void foo(int p) {
    CallbackInfo ci = new CallbackInfo();
    int a = doSomething(p + 1);
    if (p + 1 > 5) {
        return;
    }
    int b = doSomething(p);
    doSomethingTwo(a + b); 
}
```
