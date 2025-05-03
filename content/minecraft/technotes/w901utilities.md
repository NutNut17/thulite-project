---
title: "Utilities"
description: ""
summary: ""
date: 2024-10-08T19:53:05+08:00
lastmod: 2024-10-08T19:53:05+08:00
draft: false
weight: 901
toc: true
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

### Minecraft Java

#### Client

A build with improvements to run the game

- Fabric: known for its lightweight framework and quick adaptability
- Forge: is more robust and can support more extensive mods

#### Server

An additive file to host Minecraft multiplayer server

- Spigot: fork of bukkit with more feature and better performance
- Paper: fork of spigot with better performance
- Fabric Server: lightweight and performance, but incompatible with bukkit plugins

#### Plugin

Plugin is a server mods. It cannot be used on client side. Some useful plugin are as below.

| Plugin | Description |
| --- | --- |
| [LuckPerm](https://luckperms.net/) | A permission mangement plugin |
| [Dynmap](https://www.spigotmc.org/resources/dynmap%C2%AE.274/) | Show real-time view of the worlds in the server. Type `http://localhost:8123/#` into broswer to view the map |
| [Multiverse-Core](https://dev.bukkit.org/projects/multiverse-core) | A plugin to make multiple world exist in a same server |
| [Multiverse-Core Portals](https://dev.bukkit.org/projects/multiverse-portals) | Create portal between worlds |
| MultiWorld | Alternative to Multiverse-Core on fabric server |
| [WorldEdit](https://dev.bukkit.org/projects/worldedit/files) | Tool for faster building. `//wand` to get the tool |
| FAWE (FastAsyncWorldEdit) | Optimized world edit, less stable |
| VoxelSniper | Tool for distant building |
| FastAsyncVoxelSniper | Optimized VoxelSniper |
| [Dynamic Lightning](https://www.spigotmc.org/resources/basic-vanilla-server-side-dynamic-lighting.112024/) | Dynamic light when light source is hold |

Most popular plugin have alternative and updates on modern servers like fabric and paper.

**Minecraft World Browser Previewer**

Dynmap is best for cost effective 2D and 3D preview. Blue map is best for preview quality. Pl3xmap is best for performance.

{{< link-card
  title="Compare World Preview"
  description="Compare different world previews"
  href="https://map.roanv.nl/"
>}}

**LuckPerm Commands**

After the top level user permission is set, and admin group declared, run `lp user <username> parent add admin` to add user to admin group, and `lp group admin permission set pluginname.*` to enable plugin permission to admin group.

{{< link-card
  title="CPaper Chan's Hideout"
  description="Paper Chan's guide for server optimization"
  href="https://paper-chan.moe/"
>}}

#### Mods

Mods is an addon for client side.

| Mods | Platform | Descrription |
| - | - | - |
| Optifine | forge | Improves performace, supports more mods |
| Sodium | fabric | Improves FPS, `Iris` is needed to run shader |
| Phospur | fabric | light engine mod |
| Lithium | fabric | physics mod |
| Xaero's Minimap | both | Minimap that follows you, press Y for setting |
| Xaero's Map | both | World Map |
| WorldEdit | both | Tool for faster building |
| Distant Horizon | both | Render very far away chunks. Supported shaders: Photon, Complementary, Bliss, Rethinking Voxel, BSL |
| [Litematica](https://litematica.org/) | both | Tool for load and export schematics |
| [Axiom](https://axiom.moulberry.com/) | fabric | Tool for building utilities and editor |
| Immersive Portals | See through portals and teleport seamlessly |

#### Software and Website Utilities

![Modrinth](images/minecraft/util/modrinth.png)

{{< link-card
  title="Modrinth"
  description="A third-party Minecraft launcher integrating mods, shaders, datapacks, versions, etc. with a management interface."
  href="https://modrinth.com/"
>}}

---

![MCA Selector](images/minecraft/util/mcaselector.png)

{{< link-card
  title="MCA Selector"
  description="An open source software to move chunks, regions (32*32 chunks) from a Java world map to another."
  href="https://github.com/Querz/mcaselector"
>}}

---

![Amulet Editor](images/minecraft/util/amulet.png)

{{< link-card
  title="Amulet Editor"
  description="Free 3D world editor and a converter"
  href="https://www.amuletmc.com/"
>}}

---

![Universal Minecraft Tool](images/minecraft/util/umt.png)

{{< link-card
  title="Universal Minecraft Tool"
  description="A online platform that edits and converts maps more efficient, but cost a subscriptions"
  href="https://www.universalminecrafttool.com/features/converter"
>}}

---

![Seeder](images/minecraft/util/seeder.png)

{{< link-card
  title="Seeder"
  description="A website to preview terrain"
  href="https://www.mcseeder.com/"
>}}

---

![MC Map ItemTool](images/minecraft/util/mcmap.png)

Create map in the game, then convert the image into a map generated in website, then replace the map to the original map in the game

{{< link-card
  title="MC Map ItemTool"
  description="A website converts image to minecraft map nbt files"
  href="https://mc-map.djfun.de/"
>}}

---

![Cubical](images/minecraft/util/cubical.png)

{{< link-card
  title="Cubical"
  description="A website converts minecraft map into 3D schematic file"
  href="https://cubical.xyz/"
>}}

---

![Objmc](images/minecraft/util/objmc.png)

{{< link-card
  title="Objmc"
  description="A website converts 3D objects into minecraft object"
  href="https://github.com/Godlander/objmc"
>}}

#### Texture Pack

An improvement to blocks texture. An example is Cubed Texture. It a modern themed texture pack. Learn more about [Cubed Texture Pack](https://www.curseforge.com/minecraft/texture-packs/cubed-textures) at CurseForge. Also, leatn more about Cubed Texture pack and building tutorial on my favourite YouTuber [Alphine](https://www.youtube.com/@Alpine1)

#### Minecraft Skin

Some free minecraft skin sources.

{{< card-grid >}}
  {{< link-card title="Skindex" href="https://www.minecraftskins.com/" >}}
  {{< link-card title="NameMC" href="https://namemc.com/minecraft-skins" >}}
{{< /card-grid >}}

#### NCUE Minecraft Server

NCUE Minecraft server [link](https://ncuesa.ncue.edu.tw/bin/home.php)

School Public IP: `60.248.51.153`

Port(Default): `25565`

### Minecraft Bedrock

Coded in `C++`, have great performance. Playable on Mobile and Desktop. Supports NVIDIA RTX GPU ray tracing, have great performance. However, the community resource is lesser and incompatible with Minecraft Java.

#### Addons

Addon like mods, resource pack, maps, RTX mods are available on Minecraft bedrock specific platform [MCPEDL](https://mcpedl.com/)

#### Ray Tracing Packs

These are combination of shaders and texture packs using path tracing only available for Minecraft Bedrock on deviced with NVIDIA RTX graphics card. Most packs have addon packs to enhance the gaming experience.

**Kelly's RTX**

![Kelly's RTX](images/minecraft/util/rtxkelly.png)

**Vanilla RTX**

![Vanilla RTX](images/minecraft/util/rtxvanilla.png)

**Defined RTX**

![Defined RTX](images/minecraft/util/rtxdefined.png)

**RealSource RTX**

![RealSource RTX](images/minecraft/util/rtxrealsource.png)

Ashminggu is my favourite creator that creats Malaysia specific roadsign mods and vehicles mods at MCPEDL

#### Structure Block

A mod that enable the use of structure block made by [chronicoverride](https://youtu.be/Mp4_c51VDT0?si=8Zb9dg4xCm4KZTHJ).

How to use:

1. Export the structure into a mcstructure file using structure block
 in the game.
2. Move the mcstructure files into the directory `\MyStructures\structures`.
3. Zip the file `MyStructures` and change the extension to `.mcpack`.
4. Make sure the addon is removed or deleted from the game.
5. Double click the mcpack to import the structure and add the addon to the world you want to import the structure
