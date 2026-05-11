# Name

Using `name` is only viable in 26.1+ as the game is no longer obfuscated and we have local variable names.

When specifying a local variable, like when [capturing locals](https://mixins.microcontrollers.dev/mixinextras/sugar/local) or using [`ModifyVariable`](https://mixins.microcontrollers.dev/default/modifyvariable), it is much easier and safer to use the variable name, rather than counting ordinals/indices, which will change through Minecraft updates. McDev should allow autocompletion of all names.

For example, if we had a variable name, conveniently named variableName, we can very easily capture it like so:

```java
@Local(name = "variableName") int variableName
```

# Migrating

If you are moving from older versions, McDev should automatically flag these and provide you with easy one-click conversions.
