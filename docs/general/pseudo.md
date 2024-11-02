# Pseudo

When attempting to mixin into a class that may not exist at runtime, say, when you are mixining into another mod, the mixin will usually cause a crash. This can be avoided by using `@Pseudo`.

```java
@Pseudo
@Mixin(OtherMod.class)
public class OtherModMixin {
    ...
}
```
