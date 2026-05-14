# WrapMethod

!!! info
    For a more in-depth explanation, see the [MixinExtra's Wiki](https://github.com/LlamaLad7/MixinExtras/wiki/WrapMethod).

`WrapMethod` is somewhat similar to [`WrapOperation`](https://mixins.microcontrollers.dev/mixinextras/wrapoperation), except instead of wrapping a method call, we wrap the entire method itself.

Let's say we have a method called foo:

```java
@WrapMethod(method = "foo")
private void foo(Operation<Void> original) {
    original.call()
}
```

Obviously, this by itself does nothing, we just call the original method. However, we are able to wrap the method however we please. We can write code to run before and after, we can replace the method entirely, or we can conditionally wrap the method as well.

!!! warning
    Not calling `original.call()` means you are essentially overwriting the method entirely. Make sure this is only done deliberately and full consideration of alternatives is considered.

## Rationale

Say we wanted to [`Inject`](https://mixins.microcontrollers.dev/default/inject) at the `HEAD` and `TAIL` of a method. A popular example of this is pushing a pose at the beginning and manipulating the pose, then popping at the end of the method. This will have major issues if another mod `cancel`s the method somewhere inbetween. Now, our pose pop no longer runs, and we have a wild pose running around. By using `WrapMethod`, we ensure that all of our code runs, as once the original method completes (or is canceled), our code runs.

```java
@WrapMethod(method = "foo")
private void foo(GuiGraphicsExtractor graphics, Operation<Void> original) {
    graphics.pose().pushMatrix();
    ...
    original.call(graphics);
    graphics.pose().popMatrix();
}
```
