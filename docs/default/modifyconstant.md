# ModifyConstant

!!! warning
    ModifyConstant causes hard conflicts with any other mods trying to change the same constant and should be avoided when possible. You can usually receieve a similar result with a ModifyExpressionValue (TODO: create and link).

`ModifyConstant` allows easy editing of a constant anywhere in a method.

Say we had the following code:

```java
public void foo() {
    int x = this.getWidth() + 5;
    int y = this.getHeight() + 10;
    drawTexture(x, y);
    drawTexture2(x - 20, y - 20);
}
```

If we wanted to translate both the textures along the `y`, we could simply do so by modifying the constant from the `+ 5`:

```java
@ModifyConstant(method = "foo", constant = @Constant(intValue = 5))
private int changeConstant(int original) {
    return 15;
}
```

To result in:

```java
public void foo() {
    int x = this.getWidth() + 15;
    int y = this.getHeight() + 10;
    drawTexture(x, y);
    drawTexture2(x - 20, y - 20);
}
```

This example could obviously be solved in many different ways as well, but `ModifyConstant` also allows us to modify numbers that would usually be difficult to target.

Say we had a for loop as so:

```java
for (int i = 0; i < 10; i++) {
    ...
}
```

We could use a `ModifyConstant` here to target the intValue 10 to change it to whatever we wanted.
