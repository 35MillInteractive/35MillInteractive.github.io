# Work Log

Weekly notes from solo development. Add each new week directly under this intro, newest first.

## 🛠️ Work Log: Week of Oct 10 – Oct 16, 2026

Solo development on **Crownlands**, a Conan Exiles mod built in the Unreal Engine DevKit, plus the art and VFX pipeline behind it.

### Highlights
- **Homepoint Crystals V2 shipped** alongside **Dungeon Master's Spoils V2**, announced to the community with a gameplay demo of the new Shatter system.
- **Elemental unlock VFX** built nearly end to end in Niagara, then re-themed into a second branch (Arcane) using the same template.
- **Lore pipeline** consolidated into a single master lore bible, with community lore posts brought back in line with it.

### What I built
**Homepoint Crystals (gameplay and networking)**
- Public and private (clan) homepoint crystals working end to end.
- A **Shatter** option for non-owners on private crystals, so a private respawn point can't become an unkillable forward base in PvP. It's a custom entry on the hold-to-interact radial wheel, routed from the client to the server through a Run on Server event on a player-owned component, finishing with sound and VFX. A small material refund on shatter is in progress.
- Fixed the crystal's interaction particles in multiplayer by multicasting at world location instead of relative location.
- Split homepoint crystals out into their own standalone mod with its own mod controller.

**Placeables and materials**
- Fixed a light flicker on my crystal sconces by making a custom copy of the game's light toggle component with the step that hid the mesh removed.
- Moved crystal hover and spin out of Blueprint timelines into one shared material (World Position Offset), so every placed crystal animates on the GPU and independently.

**Unlock VFX (Niagara)**
- `NS_Unlock_Elemental`, a three-phase effect (Gather, Burst, Imprint): swirling element-colored motes, a flat shockwave ring, velocity-aligned ember streaks, tumbling rock debris (modeled in Houdini) with cooling hot edges, and a scorch decal with radial crater cracks made in Substance Designer.
- A recolorable sigil: grayscale masks built in JangaFX IlluGen, channel-packed into RGBA textures, and driven by one master material meant to be instanced per branch.
- `NS_Unlock_Arcane`, a cool blue, violet, and cyan re-theme of the Elemental effect, with rune-ring elements up next.

**Character and texture prep**
- Located and organized the game's full-body base meshes for upcoming outfit work, and mapped how the game's modular body parts line up with armor slots.
- Started a procedural Substance Designer retexture of a fire crystal, driven by high-to-low-poly bakes (normal, thickness, curvature, AO, position) so it reads well from every angle.

**Worldbuilding**
- Stood up a single master lore bible as the source of truth for the setting and refreshed the community's nation lore posts and channels to match it.

### Skills picked up this week
- **Niagara:** custom sprite facing for ground rings, burst emitters, velocity-aligned sprites, mesh renderer debris with collision, Niagara-driven deferred decals, curve-driven color and scale fades, random picks from a fixed color set, vortex and attraction gather motion, and Emitter State timing.
- **Materials:** Set Material Attributes for injecting World Position Offset into an existing chain, Particle Color emissive rules (opaque vs. translucent), channel-packed mask materials, and hue keying for emissive masks.
- **Networking and Blueprints:** client vs. server debugging, Run on Server relays on player-owned components, owner checks on placeables, and custom radial menu options bound to click events.
- **Modding:** editing a copied engine component inside the mod, granting items from Blueprint, and splitting a feature into its own mod.
- **Texturing:** radial crack masks in Substance Designer, grayscale sigils and multi-mask export in IlluGen, and high-to-low-poly baking.

### Tools
Unreal Engine (Conan Exiles DevKit), Niagara, Houdini, Substance Designer, Substance Painter, JangaFX IlluGen
