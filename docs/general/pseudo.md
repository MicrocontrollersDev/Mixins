# Pseudo

When attempting to mixin into a class that may not exist at runtime, say, when you are mixining into another mod, the mixin will usually cause a crash. This can be avoided by using `@Pseudo`.

```java
@Pseudo
@Mixin(targets = "com.example.mod.OtherMod")
public class OtherModMixin {
    ...
}
```

When using `@Pseudo` you should use targets and not a direct class reference.
