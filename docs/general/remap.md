# Remap

Since Minecraft is no longer obfuscated as of 26.1, this is pretty much unnecessary. If you are on an older version, as Mixin is usually set to remap by default, if we want to do mixin into, say another mod, it probably won't be obfuscated either. So in these cases, we want to skip remapping by simply appending `remap = false` to the end of our annotation.

```java
@Inject(method = ..., at = @At(...), remap = false)
```

The best way to tell if setting this is required is to simply test it yourself in prod. If it crashes, the error message should (hopefully) tell you its a remapping issue.
