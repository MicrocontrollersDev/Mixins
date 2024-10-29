# ModifyArgs

`ModifyArgs` provides a simple way to change multiple arguments of a method call.

Say we had the following code:

```java
public void foo(float f) {
    String a = param.toString();
    int b = f / 4;
    doSomething(a, b, f);
}
```

Let's say we wanted to change b and f to multipliplied by 2 instead. Since the variables are only used in the doSomething call, we can `ModifyArgs` the call:

```java
@ModifyArgs(method = "foo", at = @At(value = "INVOKE", target = "doSomething(Ljava/lang/String;IF)V"))
private void changeMethodParams(Args args) {
    int b = args.get(1); // gets the 1st (0-indexed) variable
    float f = args.get(2); // gets the 2nd (0-indexed) variable
    int newB = b * 2;
    int newF = f * 2;
    args.set(1, newB); // sets the 1st (0-indexed) variable
    args.set(2, newF); // sets the 2nd (0-indexed) variable
    // this code can obviously be simplified down
}
```

This results in:

```java
public void foo(float f) {
    String a = f.toString();
    int b = f / 4;
    doSomething(a, b / 2, f / 2);
}
```

Remember that args.get(index) and args.set(index) are 0-indexed!