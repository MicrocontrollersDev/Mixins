# Ordinals

Let's say there exist several of a method we are attempting to inject at as below:

```java
public void foo() {
    int a = doSomething(1);
    int b = doSomething(2);
    int c = doSomething(3);
}
```

If we wanted to `Redirect` doSomething(2) specifically, this can be done using an ordinal:

```java
@Redirect(method = "foo", at = @At(value = "INVOKE", target = "doSomething(I)I"), ordinal = 1)
private void redirectSomething(int original) {
    return doSomethingElse(original);
}
```

Which results in:

```java
public void foo() {
    int a = doSomething(1);
    int b = redirectSomething(2);
    int c = doSomething(3);
}
```

Ordinals are 0-indexed, meaning the first instance of a method will have an ordinal of 0, the second will have an ordinal of 1, and so on.

If you wish to target all instances of the method call, simply leave out the ordinal and mixin will target all of them. If you wish to target multiple but not all, you must either repeat the injection with each ordinal or use slices. TODO: create and link slices page
