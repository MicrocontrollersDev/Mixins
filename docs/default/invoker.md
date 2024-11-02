# Invoker

`Invoker`s allow you to invoke a method call, regardless of if it is private. This allows us to bypass needing to use an access widener or access transformer in some cases.

Say we had the following class:

```java
public class Render {
    public void drawTexture(ResourceLocation texture, int x, int y) {
        drawTexure(texture, x, y, -1);
    }

    private void drawTexture(ResourceLocation texture, int x, int y, int color) {
        ...
    }
}
```

If we wanted to call drawTexture with color in another mixin (not in RenderMixin), we could get around the issue of it being private by declaring an invoker like so:

```java
@Mixin(Render.class)
public interface RenderInvoker { // invoker methods are interfaces!!!
    @Invoker
	void invokeDrawTexture(ResourceLocation texture, int x, int y, int color);
}
```

And we would be able to access this method like:

```java
@Inject(method = "foo", at = @At("HEAD"))
private void drawOurTexture(Render renderInstance, CallbackInfo ci) {
    ((RenderInvoker) renderInstance).invokeDrawTexture(this.texture, this.x, this.y, this.color);
}
```

TODO: Static invokers
