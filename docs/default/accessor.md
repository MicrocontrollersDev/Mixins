# Accessors

`@Accessor`s allow us to get and set private target fields without needing to use an access widener or access transformer in most cases.

Say the following class existed:

```java
public class Dummy {
    private int dummyField;
    ...
}
```

We can create accessors for both getter and setters as so:

```java
@Mixin(Dummy.class)
public interface AccessorMixin { // accessor classes are interfaces!!!
	@Accessor("dummyField")
	int modid$getDummyField();

	@Accessor("dummyField")
	void modid$setDummyField(int value);W
}
```

We can then use these like so:

```java
public void myMethod() {
    // Getting the field
    int i = ((AccessorMixin) Dummy.getInstance()).modid$getDummyField();

    // Setting the field
    ((AccessorMixin) Dummy.getInstance()).modid$setDummyField(i + 1);
}
```

It's important to note that we should be prefixing our accessors with our mod id to prevent crashes.

Also, make note again that the class type is an Interface for the accessor Mixin. This means that even if we already have a Mixin for this class for regular injections, we would need a second Mixin for this class for accessors.

This page is based off of [dblsaiko's Mixin Cheat Sheet](https://github.com/dblsaiko/mixin-cheatsheet) page for Accessors.
