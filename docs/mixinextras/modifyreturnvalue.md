# ModifyReturnValue

!!! info
    For a more in-depth explanation, see the [MixinExtra's Wiki](https://github.com/LlamaLad7/MixinExtras/wiki/ModifyReturnValue).

Lets you easily modify the return value of a function.

```java
@ModifyReturnValue(method = "foo", at = @At(value = "RETURN"))
private int getFoo(int original) {
    return original + 1; // returns the original value +1
}
```

If a method has multiple returns, you can specify which return to target with an [`ordinal`](https://mixins.microcontrollers.dev/general/ordinal), or the last one with "`value = "TAIL`". That said, [`ordinals`](https://mixins.microcontrollers.dev/general/ordinal) are brittle, and can usually be replaced with a [`slice`](https://mixins.microcontrollers.dev/general/slice) or with an `@Expression`.

`ModifyReturnValue` should always be used over `cir.setReturnValue(cir.getReturnValue())` patterns from [`Inject`s](https://mixins.microcontrollers.dev/default/inject).