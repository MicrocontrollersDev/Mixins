# Overwrite

!!! danger
    Never use Overwrites!

This type of injection should never be used unless you want your mod to be incompatible with other mods. Overwrites are the most basic mixin. They, well, overwrite a method entirely. Great for testing code concepts or learning before transitioning your code to other injectors, but almost always terrible for production.

Say we had the following code:

```java
public void foo() {
    doSomething();
}
```

We could replace this outright as such:

```java
@Overwrite
public void foo() {
    doSomethingElse();
}
```

And of course, the result:

```java
public void foo() {
    doSomethingElse();
}
```

Obviously, these can easily cause mod compatability issues and should almost never be used. Valid use cases may be when you absolutely do not want anyone else to modify the same code for any reason (99.99% of the time, this does not hold up), or, realistically, for the sake of performance when you don't want to introduce callbacks in a hot piece of code, though you should profile using better injections first to make sure it is absolutely necessary.
