# Debug

Mixins can be super difficult to understand at first. Even experienced users may want to check how their mixin ended up getting applied for more complicated injections. Thankfully, Mixin supports simple debugging to do just this.

To debug, simply add `@Debug(export = true)` above your mixin class.

Example:

```java
@Debug(export = true)
@Mixin(Minecraft.class)
public class MinecraftMixin {
    ...
}
```

This will generate a .class file in `/run/.mixin.out` that you can simply throw in a decompiler to check how the final class looks like with your mixin applied.

## Project Wide Debugging

If you want to debug ALL your mixins, you can add the JVM argument `-DMixin.debug.export=true` to your run config's VM options.
