# Slice

Slices allow you to specify a section of code you want to mix into.

Say we have the following code:

```java
private void foo() {
    // ignoring any method parameters
    renderTexture(); // 0
    renderTexture(); // 1
    renderTexture(); // 2
    renderTexture(); // 3
    renderTexture(); // 4
}
```

If we only wanted to target the 1st and 2nd (0-indexed) `renderTexture` call, rather than writing several injections, we can target the call and slice only the section we want. In this case if we want to slice after the 1st and before the 3rd (0-indexed)

```java
@WrapOperation(method = "foo", at = @At(value = "INVOKE", target = "renderTexture()V", slice = @Slice(
        from = @At(value = "INVOKE", target = "renderTexture()V", ordinal = 1),
        to = @At(value = "INVOKE", target = "renderTexture()V", ordinal = 3)
    ))
)
private void renderDifferentTexture() {
    return renderMyTexture();
}
```

```java
private void foo() {
    // ignoring any method parameters
    renderTexture(); // 0
    // sliced here
    renderMyTexture(); // 1
    renderMyTexture(); // 2
    // sliced here
    renderTexture(); // 3
    renderTexture(); // 4
}
```

While method parameters were excluded for simplicity, your targetted methods will likely have special parameters that can be distinctly targetted. In this case, it may be more appropriate to use an `@Expression` to more specifically target calls we want, if applicable.
