# Mixins
!!! warning This page is a very heavy work in progress. Some pages have been mostly completed, some are still in progress, and many have no work started.

## What are they?

Mixins are one of the most powerful, but dangerous tools in the entierity of the Minecraft modding scene, always remember this quote:

> "With Great power, comes great responsibility"

## Oh the posibilities

You can basically do anything with mixins, from just adding a hook to Minecraft code to overriding entire methods with your own from the Minecraft source to even other mods.

## What about other mods?

When making mixins, always put mod compatiblity first, for example, if you override a method which another mod injects into, you at best break the other mods feature, and at worst break the whole Minecraft instance.

Thats why you can't just override every single method, even if the code you put in is identical to the previous one, that's why you have to do all the fancy stuff listed in the rest of this cheat-sheet!

> "Good mod compatibility ensures a happy mind" *or something*
