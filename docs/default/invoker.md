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
    @Invoker("drawTexture")
	void modid$invokeDrawTexture(ResourceLocation texture, int x, int y, int color);
}
```

And we would be able to access this method like:

```java
@Inject(method = "foo", at = @At("HEAD"))
private void drawOurTexture(Render renderInstance, CallbackInfo ci) {
    ((RenderInvoker) renderInstance).modid$invokeDrawTexture(this.texture, this.x, this.y, this.color);
}
```

While prefixing accessors with our modid is not strictly required if they are static or if the name you chose doesn't already exist in the target method or any other mods that may add it, it is the best way to ensure that there are no collisions, and I recommend you add them unless you know they are not required.

Remember that we can only have one method with the same name, parameters, and return type in a class. This is why we prefix our invoker method with "invoke" or "call" as these are the only two prefixes Mixin supports as mentioned in the comments. As long as we use these prefixes with the same method name in the target class, Mixin will automatically find it without specifying in the annotation.

```java
@Mixin(Render.class)
public interface RenderInvoker {
    @Invoker
	void invokeDrawTexture(ResourceLocation texture, int x, int y, int color); // this method *must* be called invoke[METHOD] or call[METHOD]
}
```

Also, make note again that the class type is an Interface for the invoker Mixin. This means that even if we already have a Mixin for this class for regular injections, we would need a second Mixin for this class for invokers.

TODO: Static invokers
