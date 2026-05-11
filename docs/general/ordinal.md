# Ordinals

!!! warning
    Ordinals should typically be avoided, especially as you target higher value ordinals. They are inherently brittle as they can change between Minecraft versions, and it can be difficult to see at a glance that you are now targetting the wrong ordinal without actually testing your feature. In general, if you can avoid using an ordinal via a different injection type, it would be advisable to do so. Ordinals can also almost always be avoided with the use of `Expression`s or `Slice`s.

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
private int redirectSomething(TargetClass instance, int original) {
    return doSomethingElse(original);
}
```

Which results in:

```java
public void foo() {
    int a = doSomething(1);
    int b = doSomethingElse(2);
    int c = doSomething(3);
}
```

Ordinals are 0-indexed, meaning the first instance of a method will have an ordinal of 0, the second will have an ordinal of 1, and so on.

If you wish to target all instances of the method call, simply leave out the ordinal and mixin will target all of them. If you wish to target multiple but not all, you must either repeat the injection with each ordinal or use slices. TODO: create and link slices page
