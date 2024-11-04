# Coerce

`Coerce` allows you to set the type of a mixin method argument to Object. This allows us to bypass any issues with method parameters for our mixins.

Say we had a mixin like so:

TODO: check if method signature makes sense

```java
@WrapOperation(method = "foo", at = @At(value = "INVOKE", target = "doSomething(LPrivateClass;II)V"))
private void doSomethingElse(PrivateClass param, int x, int y) {
    doThisInstead(x, y);
}
```

Let's say PrivateClass is private. Now, this mixin will not work, even though we don't even use the parameter in our mixin at all. We could write an access widener or access transformer, or we can use `Coerce` to coerce it into a different object.

```java
@WrapOperation(method = "foo", at = @At(value = "INVOKE", target = "doSomething(LPrivateClass;II)V"))
private void doSomethingElse(@Coerce Object param, int x, int y) {
    doThisInstead(x, y);
}
```

This will now build and work as expected! `Coerce` should only be used if the type you are coercing doesn't need to be used in the mixin.

## Coercing Return Types

TODO: I didnt know this was possible until just now, needs review and example

`Coerce` can also be used to coerce the return type of a mixin, however, much more limited. This only works with [`Inject`](https://mixins.microcontrollers.dev/default/inject) and [`Redirect`](https://mixins.microcontrollers.dev/default/redirect).
