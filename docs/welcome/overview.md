# Mixins

!!! example "WIP"
    This site is a very heavy work in progress. Some pages have been mostly completed, some are still in progress, and many have no work started.

## What is this?

This is a cheatsheet-like guide to help explain the basics of using mixins for Minecraft modding. This guide will go over all of the different injections, the basics of using them, when to use them, and provide examples to make it as clear as possible as to how they operate.

This guide will **not** teach you the basics of bytecode or what is actually happening on the bytecode level. It is a broad overview to get you started writing mixins. If you want to learn more about that, you should read the official [Sponge Mixin Wiki](https://github.com/spongepowered/mixin/wiki).

For someone completely new to Mixins, this guide may appear out of order or all over the place. I have tried to make this guide have explanations by example, rather than a giant javadoc to read. You may need to swap between certain pages to understand how something works. For example, the page for [`Shift`ing](https://mixins.microcontrollers.dev/general/shift) uses [`Inject`s](https://mixins.microcontrollers.dev/default/inject), but if reading in order, you won't know what an Inject is until later. If a word is not immediately clear, try to see if another page exists detailing it

Lastly, this guide is meant to be a general guide targeted towards new users or those who just need a refresher. There are a lot of cool and wacky things you can do with Mixins, weird injections, weird usecases, but those may not be covered (feel free to open and issue & PR if you feel inclined to write anything, however).

## What are they?

Mixins are one of the most powerful, but dangerous tools in the entierity of the Minecraft modding scene. Unlike your typical Forge or Fabric API events, mixins are direct modification of the Minecraft code using ASM. Our mixin classes aren't typical classes - at runtime, they will directly modify Minecraft's code. Due to the power of mixins, it's important to write good code that ensures mod compatability.

> "With Great power, comes great responsibility"

## What about other mods?

When making mixins, always put mod compatiblity first. If you poorly override a method which another mod injects into, you at best break the other mods feature, and at worst break the whole Minecraft instance.

Thats why you can't just override every single method, even if the code you put in is identical or near identical to the previous one. Throughout this guide/cheatsheet, tips will be provided on when and how to use certain injections, which should help aid in compatability.

Remember, the cleaner your mixin is, the better. Only modify what you have to, and try to change as little of Minecraft's code as possible.
