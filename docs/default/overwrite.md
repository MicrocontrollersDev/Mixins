# Overwrite

!!! warning Overwriting is not recommended.

Overwrites are the most basic mixin. They, well, overwrite a method entirely.

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

Obviously, these can easily cause mod compatability issues and should almost never be used. Valid use cases may be when you absolutely do not want anyone else to modify the same code for any reason, or for the sake of performance when you don't want to introduce callbacks in a hot piece of code.

However, for most users, avoid using overwrites.
