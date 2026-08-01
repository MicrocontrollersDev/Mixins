# ModifyReceiver

!!! info
    For a more in-depth explanation, see the [MixinExtra's Wiki](https://github.com/LlamaLad7/MixinExtras/wiki/ModifyReceiver).

Say we had a class:

```java
private void foo() {
    ...
    bar.setBar(newBar);
    ...
}
```

And we want to replace the receiver outright. We can do:

```java
@ModifyReceiver(method = "foo", at = @At(value = "INVOKE", target = "setBar(I)V"))
private void changeReceiver(Bar bar, int newBar) {
    if (newBar > 0) {
        return quux;
    } else {
        return bar;
    }
}
```

With this, we have conditionally replaced the receiver for the `setbar` call:

```java
private void foo() {
    ...
    if (newBar > 0) {
        quux.setBar(newBar);
    } else {
        bar.setBar(newBar);
    }
    ...
}
```

This page is directly based off of [LlamaLad7's MixinExtra Wuju](https://github.com/LlamaLad7/MixinExtras/wiki/ModifyReceiver) page for ModifyReceivers.
