# Require

Depending on your mod template, you may have noticed a "defaultRequire", usually set to 1. This means that by default all mixins must apply correctly, or else your mod will crash. This is usually what you want, if your mod isn't applying mixins correctly, something is wrong, and a crash is expected. However, there may be some cases where you don't really care whether a mixin applies or not, especially when it comes to mod compatibility.

Mixing into another mod is inherently brittle since while Minecraft's code isn't going to change for whatever version you target, other mods can. There may be cases where mod compatibility is not a big deal (e.g., just a small visual error that does not warrant a full blown crash). In these cases, we can add a `require = 0` to the injector to allow your mixin to fail without crashing the game.

```java
@Inject(method = ..., at = @At(...) require = 0)
```
