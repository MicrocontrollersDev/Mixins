# Invoker

`@Invoker`s allow you to invoke a method call, regardless of if it is private. This allows us to bypass needing to use an access widener or access transformer in most cases.

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

If we wanted to call drawTexture with color in another mixin (not in RenderMixin), we could get around the issue of it being private by declaring an invoker by creating an interface class like so:

```java
@Mixin(Render.class)
public interface RenderInvoker { // invoker classes are interfaces!!!
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

Remember that we can only have one method with the same name, parameters, and return type in a class. This is why we prefix our invoker method with "invoke". Mixin allows prefixing with either "invoke" or "call", but one of them must be used.

Also, make note again that the class type is an Interface for the invoker Mixin. This means that even if we already have a Mixin for this class for regular injections, we would need a second Mixin for this class for invokers.

TODO: Static invokers
