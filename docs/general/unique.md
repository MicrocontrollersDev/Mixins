# Unique

Sometimes we want to create a new method or variable in our mixin class. In order to tell Mixin that we do not want this method or field to possibly overwrite any other method or field that could exist, we mark them with a `@Unique` annotation. This is incredibly important for mod compatibility, in a case where two mods try to create a method/field with the same name.

While `@Unique` on its own should prevent most mod conflicts, it is recommended to still prefix your method/field with your modid (e.g., modid$methodName). `@Unique` only attempts to prevent overlaps when it detects that two mods will collide, and this detection is not perfect.

There are two cases that I know of:

1. If you use `@Unique` and your mod gets applied first, but a second mod gets applied later and doesn't use `@Unique`, they will collide.

2. While rare, this can be triggered in weird ways, such as kotlin companion objects or java interfaces in which the variables are declared outside the mixin class. Always prefix these variables with your mod id if they are intended to be used within mixin classes.
