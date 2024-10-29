# ModifyArg

`ModifyArg` provides a simple way to change a single argument of a method call.

Say we had the following code:

```java
public int foo(float f) {
    String a = f.toString();
    int b = f / 4;
    doSomething(a, b, f);
    return b + 5;
}
```

Let's say we wanted to change b to be b / 2 instead **only** in the doSomething call. We can `ModifyArg` the call using the correct index:

```java
@ModifyArg(method = "foo", at = @At(value = "INVOKE", target = "doSomething(Ljava/lang/String;IF)V"), index = 1) // gets the 1st (0-indexed) variable
private int changeMethodParam(int b) {
    return b / 2;
}
```

This results in:

```java
public void foo(float f) {
    String a = f.toString();
    int b = f / 4;
    doSomething(a, b / 2, f);
    return b + 5
}
```

Remember that index is 0-indexed!
