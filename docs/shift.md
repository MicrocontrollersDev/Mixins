# Shift

There are three types of Shifts: Before, After, and By.

## After

Mixin injections happen the line before a method is called. So, what do we do if we want to inject *after* a method call?

Say we had the following method:

```java
public void foo() {
    doSomething1();
    doSomething2();
    doSomething4();
}
```

Let's say we wanted to call doSomething3() after doSomething2. This could be done as such:

```java
@Inject(method = "foo", at = @At("INVOKE", target = "doSomething2()V", at = At.Shift.AFTER))
private void doSomethingAfter() {
    doSomething3();
}
```

This gives us the following code:

```java
public void foo() {
    doSomething1();
    doSomething2();
+   doSomething3();
    doSomething4();
}
```

## Before

Before is not recommended.

TODO: write this section

## By

By is not recommended.

TODO: write this section

## Practical Example

Shifts have many practical use cases. Say we had the following code:

```java
public void render(ResourceLocation guiTexture, ResourceLocation otherTexture) {
    if (shouldRenderGui()) {
        drawGuiTexture(guiTexture);
    }
    else if (shouldRenderOther()) {
        drawOtherTexture(otherTexture)
    }
}
```

And we want to surround only the drawGuiTexture call in calls to RenderSystem.setShaderColor to overlay a color or apply opacity. However, we want to reset the shader color before rendering anything else. To do this, we can surround the drawGuiTexture call with our first regular `Inject`, and a second shifted `Inject` as so:

```java
@Inject(method = "render", at = @At("INVOKE", target = "drawTexture(Lnet/minecraft/resources/ResourceLocation)V"))
private void drawGuiTexturePre() {
    RenderSystem.setShaderColor(1f, 1f, 1f, 0.5f); // set an alpha of 0.5
}

@Inject(method = "render", at = @At("INVOKE", target = "drawTexture(Lnet/minecraft/resources/ResourceLocation)V", at = At.Shift.AFTER))
private void drawGuiTexturePost() {
        RenderSystem.setShaderColor(1f, 1f, 1f, 1f); // reset alpha after drawing the texture
}
```

This would result in the following code:

```java
public void render(ResourceLocation guiTexture, ResourceLocation otherTexture) {
    if (shouldRenderGui()) {
+       RenderSystem.setShaderColor(1f, 1f, 1f, 0.5f);
        drawGuiTexture(guiTexture);
+       RenderSystem.setShaderColor(1f, 1f, 1f, 1f);
    }
    else if (shouldRenderOther()) {
        drawOtherTexture(otherTexture)
    }
}
```