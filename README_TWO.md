# Mindustry Modding Guide

This guide provides an updated overview of how to create mods for Mindustry, based on the latest official documentation.

## Introduction to Modding

Mindustry mods are essentially directories of assets. You can do many things with the modding API, from simply re-spriting existing content to creating new blocks, items, units, and even adding custom game logic with scripts.

Sharing your mod is as simple as sharing the project directory. Mods are cross-platform, and using a service like GitHub is recommended for hosting and collaboration.

## Directory Structure

A typical mod project has the following directory structure:

```
your-mod-name/
├── mod.hjson
├── content/
│   ├── items/
│   ├── blocks/
│   ├── liquids/
│   └── units/
├── maps/
├── bundles/
├── sounds/
├── schematics/
├── scripts/
├── sprites-override/
└── sprites/
```

- **`mod.hjson`** (Required): Metadata file for your mod.
- **`content/`**: Contains the JSON/HJSON definitions for your custom content.
- **`maps/`**: For custom in-game maps.
- **`bundles/`**: For translations and custom text.
- **`sounds/`**: For custom sound files (OGG or MP3).
- **`schematics/`**: For `.msch` schematic files.
- **`scripts/`**: For custom game logic using JavaScript.
- **`sprites-override/`**: For overriding vanilla game sprites.
- **`sprites/`**: For your mod's custom sprites.

### Mod Installation Paths
- **Linux**: `~/.local/share/Mindustry/mods/`
- **Steam**: `steam/steamapps/common/Mindustry/saves/mods/`
- **Windows**: `%appdata%/Mindustry/mods/`
- **MacOS**: `~/Library/Application Support/Mindustry/mods/`

## The `mod.hjson` File

This file contains essential metadata for your mod.

```hjson
# The internal name of your mod. Should be unique and in kebab-case.
name: "my-awesome-mod"

# The display name of your mod in the game. Can use color formatting.
displayName: "My Awesome Mod"

# Your name.
author: "Your Name"

# A short description of your mod.
description: "This mod adds new and exciting content to Mindustry."

# The version of your mod.
version: "1.0"

# The minimum game version required to run this mod.
minGameVersion: "146"

# A list of other mods that this mod depends on.
dependencies: []

# If true, the mod is not required for clients on a server to join.
# Good for texture packs or UI mods. Set to false for content mods.
hidden: false
```

## Creating Content

Content is defined in HJSON format (a more human-friendly version of JSON). Files are placed in the respective subdirectories of the `content/` folder (e.g., `content/blocks/my-new-turret.hjson`).

The filename (without extension) is used as the internal name of the content. For example, `my-new-turret.hjson` creates a block named `my-new-turret`.

Here's a basic example of a custom block:

```hjson
type: Wall
name: "My Awesome Wall"
description: "A very awesome wall."
health: 200
size: 1
requirements: [
  copper/6
]
category: defense
research: copper-wall
```

### Content Types

The `type` field is crucial. It determines what kind of content you are creating. Some common types include:
- **Blocks**: `Wall`, `Turret`, `Drill`, `Conveyor`, etc.
- **Items**: `Item`
- **Liquids**: `Liquid`
- **Units**: `flying`, `mech`, `naval`

Types can be extended. For example, a `MissileBulletType` extends `BasicBulletType`, inheriting its properties.

## Sprites

- Sprites must be **32-bit RGBA PNG** files.
- Block sprites should be `32px * size`. For a 2x2 block, the sprite should be 64x64px.
- Place your sprites in the `sprites/` directory. The game will automatically associate a sprite with content of the same name (e.g., `sprites/my-new-turret.png` for the `my-new-turret` block).

## Sounds

- Custom sounds can be added to the `sounds/` directory.
- Supported formats are **OGG** and **MP3**. OGG is recommended for looping sounds.
- Reference sounds by their filename (without extension).

## Sharing Your Mod

The easiest way to share your mod is via GitHub.
1. Create a GitHub repository for your mod.
2. Push your mod files to the repository.
3. Add the `mindustry-mod` topic to your repository to make it discoverable.
4. Players can then import your mod in-game by entering `YourUsername/YourRepositoryName`.

## Further Reading

This guide covers the basics. For more advanced topics like scripting, custom shaders, and Java/Kotlin modding, please refer to the [Official Mindustry Modding Wiki](https://mindustrygame.github.io/wiki/modding/1-modding/).
