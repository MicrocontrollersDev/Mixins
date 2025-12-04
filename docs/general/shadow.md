# Shadow

`Shadow` lets Mixin know when you are referencing a target class's method or fields.

Say we had the following class:

```java
public class Example {
    public String example = "exampleString";

    public void foo() {
        ...
    }

    public void printString(String string) {
        System.out.println(string);
    }
    ...
}
```

If we wanted access to these in our mixin, we could do so with `@Shadow`:

```java
@Mixin(Example.class)
public class ExampleMixin {
    @Shadow
    public String example;

    @Shadow
    public void printString(String string);

    @Inject(method = "foo", at = @At("HEAD"))
    private final fooInject(CallbackInfo ci) {
        this.printString(this.example);
    }
}
```

We can use McDev to autocomplete our shadows by using `this.` and tab completing our method or field.
