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
	void modid$setDummyField(int value);
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

If we can't getInstance, we can cast to Object instead.

```java
public void myMethod(Dummy dummy) {
    // Getting the field
    int i = ((AccessorMixin) (Object) dummy).modid$getDummyField();

    // Setting the field
    ((AccessorMixin) (Object) dummy).modid$setDummyField(i + 1);
}
```

While prefixing accessors with our modid is not strictly required if they are static or if the name you chose doesn't already exist in the target method or any other mods that may add it, it is the best way to ensure that there are no collisions, and I recommend you add them unless you know they are not required. If we don't want to prefix, we can simplify the mixin.

Remember that we can only have one method with the same name, parameters, and return type in a class. This is why we prefix our accessor field with "get" or "set" as these are the only two prefixes Mixin supports as mentioned in the comments. As long as we use these prefixes with the same field name in the target class, Mixin will automatically find it without specifying in the annotation.

```java
@Mixin(Dummy.class)
public interface AccessorMixin {
	@Accessor
	int getDummyField(); // getters must be named get[NAME]

	@Accessor
	void setDummyField(int value); // setters must be named set[NAME]
}
```

Also, make note again that the class type is an Interface for the accessor Mixin. This means that even if we already have a Mixin for this class for regular injections, we would need a second Mixin for this class for accessors.

This page is directly based off of [dblsaiko's Mixin Cheat Sheet](https://github.com/dblsaiko/mixin-cheatsheet/blob/master/accessor.md) page for Accessors.
