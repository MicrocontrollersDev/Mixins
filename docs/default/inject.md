# Inject

`@Inject` is one of the simplest injections in Mixin to understand. It allows you to inject any code at any line you want (with a few exceptions).

There are two types of `@Inject`s, cancelable, and not cancelable. But first, let's talk about the main injection points. (TODO: maybe restructure this page?)

## Injecting at HEAD

Let's say we just want to add some extra code at the **beginning** of a method.

```java
public void foo() {
    System.out.println("Message 1");
    System.out.println("Message 2");
}
```

And we wanted to add a print line for "Message 0" at the beginning. We would inject at the "head" of the method.

```java
@Inject(method = "foo", at = @At("HEAD"))
private void addMessage0(CallbackInfo ci) {
    System.out.println("Message 0");
}
```

Which leaves us with:

```java
public void foo(float f) {
    System.out.println("Message 0");
    System.out.println("Message 1");
    System.out.println("Message 2");
}
```

## Injecting at TAIL

Let's say we just want to add some extra code at the **end** of a method.

```java
public void foo() {
    System.out.println("Message 1");
    System.out.println("Message 2");
}
```

And we wanted to add a print line for "Message 3" at the end. We would inject at the "head" of the method.

```java
@Inject(method = "foo", at = @At("TAIL"))
private void addMessage3(CallbackInfo ci) {
    System.out.println("Message 3");
}
```

Which leaves us with:

```java
public void foo(float f) {
    System.out.println("Message 1");
    System.out.println("Message 2");
    System.out.println("Message 3");
}
```

## Injecting at RETURN

Let's say we just want to add some extra code before a return statement.

```java
public String foo() {
    varA = this.a;
    varB = this.b;
    if (varA == varB) {
        return "True!"
    } else {
        return "False!"
    }
}
```

And we wanted to add a print, say, "Hello World!" before printing "True!". Yes, this is a dumb example, roll with it. We would inject at the first "RETURN" of the method.

```java
@Inject(method = "foo", at = @At("RETURN"), ordinal = 0) // Remember: ordinals are zero-indexed
private void printValues(CallbackInfoReturnable cir) {
    System.out.println("Hello World!");
}
```

Which leaves us with:

```java
public String foo() {
    varA = this.a;
    varB = this.b;
    if (varA == varB) {
        System.out.println("Hello World!");
        return "True!"
    } else {
        return "False!"
    }
}
```

## Injecting at INVOKE

Let's say we just want to add some extra code before a completely arbitrary line of code.

```java
public void foo() {
    this.doMethodA();
    this.doMethodB();
}
```

And we wanted to add a print between doing method A and B. We would inject by targetting the call for method B. Please note that `@Inject`ing at a target effectively makes the code appear on the line before.

```java
@Inject(method = "foo", at = @At("INVOKE"), target = "doMethodB()V") // TODO: check if this target makes sense
private void printValues(CallbackInfo ci) {
    System.out.println("Hello World!");
}
```

Which leaves us with:

```java
public void foo() {
    this.doMethodA();
    System.out.println("Hello World!");
    this.doMethodB();
}
```

## Cancelable vs Non-Cancelable

So far these examples have been non-canceling. We just add code to the code present, we do not change the flow of the method. But what if we wanted to stop this method from running? And what's with this weird CallbackInfo/CallbackInfoReturnable?

Canceling the method does what you would expect. It basically adds a return wherever we specify.

Say we wanted to cancel this method at the start:

```java
public void foo() {
    this.doMethodA();
}
```

We can simply do

```java
@Inject(method = "foo", at = @At("HEAD"), cancelable = true) // Notice we add this here! McDev should also give you a warning if you forget.
private void cancelFoo(CallbackInfo ci) {
    ci.cancel();
}
```

And this results in

```java
public void foo() {
    return;
    this.doMethodA();
}
```

But what if the method isn't void? We can't just cancel a non-void method, but we can change the return value instead. Say we had the following.

```java
public String foo() {
    String a = this.doMethodA();
    return a;
}
```

We can simply use a CallbackInfoReturnable.

```java
@Inject(method = "foo", at = @At("HEAD"), cancelable = true)
private String cancelFoo(CallbackInfoReturnable cir) { // Notice the method is no longer void, but the same type as the method we inject!
    cir.setReturnValue("New custom string!");
}
```

And that results in

```java
public String foo() {
    return "New custom String";
    String a = this.doMethodA();
    return a;
}
```

Simple! The other injection points, "TAIL", "RETURN", and "INVOKE", also work here.
