# ModifyVariable

`ModifyVariable` provides a simple way to modify a variable (crazy).

Say we had the following class

```java
public void target() {
    double original = foo() * 2.0;
}
```

If we wanted to modify the value provided to original, we could do so

```java
@ModifyVariable(method = "target", at = @At("STORE"))
private double changeVariable(double original) { // method type is double, same as the variable type
    return original * 3.0;
}
```

And this becomes

```java
public void target() {
    double original = foo() * 2.0 * 3.0;
}
```

To specify which variable to modify, you will need to use ordinals/indices, at least until we are on deobfuscated Minecraft versions.
