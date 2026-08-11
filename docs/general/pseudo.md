# Pseudo

When attempting to mixin into a class that may not exist at runtime, say, when you are mixing into another mod, the mixin will usually cause a crash. This can be avoided by using `@Pseudo`.

```java
@Pseudo
@Mixin(targets = "com.example.mod.OtherMod") // When using `@Pseudo` you should use targets and not a direct class reference.
public class OtherModMixin {
    ...
}
```

Note that this will mean that if the mod changes its class package, the mixin will silently fail. If you wish to have an optional mixin that is still required if the mod is present, you should look into using a Mixin Plugin to conditionally register/deregister your mixin.
