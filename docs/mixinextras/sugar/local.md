# Local

!!! info
    For a more in-depth explanation, see the [MixinExtra's Wiki](https://github.com/LlamaLad7/MixinExtras/wiki/Local).

!!! warning
    Locals in general can be brittle. If it can be avoided via a different injection type, try to avoid capturing locals. If not possible, using locals is perfectly fine.

`Local` lets you easily capture local variables. Unlike the default Mixin `LocalCapture`, we can instead find the variable using ordinal and index. If there is only one instance of the variable type, we can leave these out.

It is recommended to use ordinal over index typically, but occasionally, if ordinal is causing problems, use index. Use IntelliJ's bytecode viewer to find the LVT index.

## Method Args

If the local you want to capture is part of method arguments, you can use `@Local(argsOnly = true)`.

Say we had:

```java
public void foo(boolean b) {
    doSomething();
}
```

We can do:

```java
@WrapOperation(method = "foo", at = @At(value = "INVOKE", target = "doSomething"))
private void doSomethingElse(@Local(argsOnly = true) boolean b) {
    somethingElse(b);
}
```

## In Body

If we wanted to get a local variable in the method itself, we could do so as well.

Say we had the following and wanted to capture the boolean `b`:

```java
public void foo() {
    boolean a = this.a();
    boolean b = this.b();
    doSomething(a, b);
}
```

We can do:

```java
@WrapOperation(method = "foo", at = @At(value = "INVOKE", target = "doSomething(ZZ)"))
private void doSomethingElse(@Local(ordinal = 1) boolean b) {
    somethingElse(b);
}
```

## Mutability

We can also use `Local` to directly modify local variables.

To do so, we use the object's reference type instead of its actual type.

* LocalBooleanRef
* LocalByteRef
* LocalCharRef
* LocalDoubleRef
* LocalFloatRef
* LocalIntRef
* LocalLongRef
* LocalShortRef
* LocalRef\<Type\>

Say we had the following:

```java
public void foo() {
    boolean a = this.a();
    int b = this.b();
    Text c = this.c();
    doSomething(a, b, c);
}
```

We can do:

```java
@Inject(method = "foo", at = @At("HEAD"))
private void doSomethingElse(@Local LocalBooleanRef a, @Local LocalIntRef b, @Local LocalRef<Text> c, CallbackInfo ci) {
    a.set(true);
    b.set(1);
    c.set(this.getText());
}
```

This results in:

```java
public void foo() {
    boolean a = true;
    int b = 1;
    Text c = this.getText();
    doSomething(a, b, c);
}
```
