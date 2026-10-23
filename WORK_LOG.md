# Work Log

Weekly notes from solo development. Add each new week directly under this intro, newest first.

## 🛠️ Work Log: Week of Oct 17 – Oct 23, 2026

Solo development on **Crownlands**, a Conan Exiles mod built in the Unreal Engine DevKit, plus the art and VFX pipeline behind it. This week was focused on the second of four skill-unlock effects, **Arcane**, and on building reusable tools in Houdini to speed up the rest.

### Highlights
- **Arcane unlock VFX** came together in Niagara: spinning rune rings, evenly orbiting crystals, a shard burst, and my **first Niagara ribbon**, a runic trail that follows the final crystal.
- **Procedural VFX meshes in Houdini:** five crystal shard variants, a beam cylinder, and a true 3D shockwave ring, exported in one batch.
- **My first Houdini Digital Asset** (`sop_35Mill.UE5_AssetPrep`), a reusable prep tool that sizes and pivots meshes for Unreal, now loaded automatically at startup.
- **Designed the third unlock, Hallowed,** end to end, ready to build next.

### What I built
**Unlock VFX: Arcane (Niagara)**
- `T_RuneRing_01`, a rune ring texture built in JangaFX IlluGen, with the stroke thickness tuned so the detail survives while it spins.
- **Gather:** `Gather_RuneRing` lies flat and spins with per-particle speed, and `Gather_Crystals` orbits evenly spaced crystals around the player with random shard meshes and random heights.
- **Burst:** `Burst_Shards` flings crystal shards outward, tip first along their velocity, with drag and gravity.
- **Imprint:** a rune ring riding each orbiting crystal, plus `Imprint_RuneTrail`, a ribbon that trails the imprint crystal with a scrolling, channel-packed rune material (`M_RuneTrail` with a per-school instance, `MI_RuneTrail_Arcane`).
- `M_Crystal_Shard`, an additive crystal material with a Fresnel edge tint and core glow that fades with the particle.
- Sigil material fixes: scaled the sigil from its center, clamped it so it stops tiling, and tested a cheap mip-based glow against baked glow textures.

**Houdini tools and meshes**
- Modeled the meshes the unlock effects need in one session: a capped crystal shard (with the tip welded clean), an open beam cylinder, and a slanted band that reads as a 3D shockwave from any angle.
- A For-Each loop that gives every pass a new random seed and scale, names each piece, and exports all five shards (`SM_Crystal_Shard_01` to `05`) as one FBX that splits into separate meshes in Unreal.
- Scaled everything to Unreal units against a reference character, fixed UV wrap seams so panning textures don't stretch, and unwrapped the shard in RizomUV.
- Wrapped my size-and-pivot prep into a Houdini Digital Asset with promoted parameters and set up an HDA library that loads at startup.

**Unlock VFX: Hallowed (design)**
- Laid out the full effect: a gentle beam rains feathers on the player (Gather), the beam hardens and bursts as the sigil peaks (Burst), then a halo forms overhead with light radiating out while feathers drift down and disintegrate (Imprint). The feather atlas, burst sigil, and disintegration flipbook are ready; the build starts next.

### Design decisions
- **Five shard variants, not ten:** every mesh in a Niagara mesh renderer adds a draw call, and several players can unlock skills at the same time in multiplayer.
- **Batch the modeling:** build every mesh an effect family needs in one session, and always give VFX meshes UVs.
- **One master material, one instance per school,** so Arcane, Hallowed, and the rest share the same rune trail setup.

### Skills picked up this week
- **Houdini:** procedural Tube SOP modeling, Point Jitter, Match Size pivots, For-Each batch export with per-piece naming, cylindrical UVs with seam fixes, unit scaling for Unreal, and building and auto-loading a Digital Asset.
- **Niagara:** orbiting meshes with even phase spacing, per-particle random values set at spawn, mesh index binding, velocity bursts with drag and gravity, and my first ribbon emitter sampling particles from another emitter.
- **Materials:** UV scaling from center and clamping, mip-based glow (and why textures need power-of-two sizes for it), Fresnel crystal materials, and scrolling channel-packed ribbon materials.
- **IlluGen:** rune ring textures tuned for motion.

### Tools
Unreal Engine (Conan Exiles DevKit), Niagara, Houdini, RizomUV, JangaFX IlluGen

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
