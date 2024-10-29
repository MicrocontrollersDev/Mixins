# Overwrite

`Overwrite`s are the most basic mixin. They, well, overwrite a method entirely.

Obviously, these can easily cause mod compatability issues and should almost never be used.

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
