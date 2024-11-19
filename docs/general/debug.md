# Debug

Mixins can be super difficult to understand at first. Even experienced users may want to check how their mixin ended up getting applied for more complicated injections. Thankfully, Mixin supports simple debugging to do just this.

There are many debug flags you can use, but the most useful for most people is exporting.

## Exporting

To export, simply add `@Debug(export = true)` above your mixin class.

Example:

```java
@Debug(export = true)
@Mixin(Minecraft.class)
public class MinecraftMixin {
    ...
}
```

This will generate a .class file in `/run/.mixin.out` that you can simply throw in a decompiler to check how the final class looks like with your mixin applied.

It's important to note that some classes may not generate the mixin output until after they have been properly loaded. For example, if you mixin into the chat window, you may need to join a world and open chat before the file is created in your .mixin.out.

### Project Wide Debugging

If you want to debug ALL your mixins, you can add the JVM argument `-DMixin.debug.export=true` to your run config's VM options.

## Other Debugging Settings

Some people may say to turn on *all* debugging flags using `-DMixin.debug=true`. **Do not do this**. Not only does it cause a lot of overhead due to running a profiler, it can also cause mixins that would usually soft-fail in your mod or your dependencies to outright crash the game, and can cause ASM to try to analyze classes that haven't had frames computed yet.

If you want to enable other debug settings, set them manually using the flags on the [SpongePowered Mixin Wiki](https://github.com/SpongePowered/Mixin/wiki/Mixin-Java-System-Properties).
