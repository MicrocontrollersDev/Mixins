# Mixins

!!! warning
    This site is a very heavy work in progress. Some pages have been mostly completed, some are still in progress, and many have no work started.

## What is this?

This is a cheatsheet-like guide to help explain the basics of using mixins for Minecraft modding. This guide will go over all of the different injections, the basics of using them, when to use them, and provide examples to make it as clear as possible as to how they operate.

## What are they?

Mixins are one of the most powerful, but dangerous tools in the entierity of the Minecraft modding scene. Unlike your typical Forge or Fabric API events, mixins are direct modification of the Minecraft code using ASM. Our mixin classes aren't typical classes - at runtime, they will directly modify Minecraft's code. Due to the power of mixins, it's important to write good code that ensures mod compatability.

> "With Great power, comes great responsibility"

## What about other mods?

When making mixins, always put mod compatiblity first. If you poorly override a method which another mod injects into, you at best break the other mods feature, and at worst break the whole Minecraft instance.

Thats why you can't just override every single method, even if the code you put in is identical or near identical to the previous one. Throughout this guide/cheatsheet, tips will be provided on when and how to use certain injections, which should help aid in compatability.

Remember, the cleaner your mixin is, the better. Only modify what you have to, and try to change as little of Minecraft's code as possible.
