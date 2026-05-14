# ModifyExpressionValue

!!! info
    For a more in-depth explanation, see the [MixinExtra's Wiki](https://github.com/LlamaLad7/MixinExtras/wiki/ModifyExpressionValue).

TODO: finish

Just as a placeholder due to being linked in the ModifyConstant page, this is how you can easily replace the use of a ModifyConstant:

```java
@ModifyEpressionValue(method = "foo", at = @At(value = "CONSTANT", args = "intValue = 5")
```
