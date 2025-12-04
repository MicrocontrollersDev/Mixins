# Getting Started

## Mod Loaders

Both Fabric and NeoForge have amazing support for Mixins and its ecosystem. Forge, on the other hand, does not. This guide is written on the assumption that you are using either Fabric or NeoForge.

## Templates

All modern templates should have Mixin support set up and ready to go. Make sure you read any info your template gives you.

## modid.mixins.json

This file can be found in your project's resources folder. Depending on your template, this may be mixins.modid.json or similar, but it doesn't matter what it's named as long as it is specified in either your fabric.mod.json or neoforge.mods.toml file.

You should ensure that the "package" field is properly set to your mods mixin package. Please note that this package must be separate from all your non-Mixin code. Do not put any non-Mixin classes in here!

## IntelliJ Plugins

IntelliJ is recommended for writing Mixins due to the Minecraft Dev (McDev) plugin. This plugin allows for autocompleting mixin targets, and MixinExtra's Expression definitions. Additionally, it can let you know when you write a mixin that uses brittle techniques, and other general goodies. Especially as a new Mixin user, it is an essential plugin to have. See the [Minecraft Dev](https://mcdev.io) website to learn how to install. I also recommend updating to the nightly release.

Another useful plugin is [Mixin Visualizer](https://plugins.jetbrains.com/plugin/29218-mixin-visualizer), which should show you exactly what your Mixin is actually doing.

And finally, if you are trying to Mixin into another mod's Mixin, you should the McDev addon plugin, [MixinSquared](https://plugins.jetbrains.com/plugin/26828-mixinsquared). This allows you to easily write MixinSquared Mixins.
