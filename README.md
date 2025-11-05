# SpiritLinks

# Overview
- SpiritLinks turns death into a guided “ghost run” inspired by World of Warcraft.
- When players die, they become ghosts, see wayfinding to their corpse or a Spirit Healer, hear ambient ghost music, and can revive via tomb/corpse or by right-clicking a marked Healer NPC.
- Includes gentle Healer roaming, mob repulsion fields, random on-screen whispers, center-screen revive prompts, and a built-in resource-pack mini server.

# Supported Platforms / Requirements
- **Minecraft Server:** Spigot 1.12.2 (also tested on CatServer 1.12.2 modded forks)
- **API:** Bukkit/Spigot API 1.12.2-R0.1-SNAPSHOT
- **Java:** Java 8 (1.8)
- **Optional:** Vault (for money-based costs) + an economy plugin (EssentialsEco, CMI, etc.)

# Installation
**Download & Install**
- Place spiritlinks-1.0.0.jar into /plugins/.
- Start the server once to generate config.yml.
- (Optional) Install Vault and a supported economy plugin if you want currency costs.

# Resource Pack (Built-In Server)
- The plugin can serve a small zip containing the ghost music and healer voice line.
- Configure under resourcePack.* (host, port, path, and publicHost).
- Clients will be prompted automatically if autoPushToPlayers: true.

# Quick Start (Admin)
- Set the Cemetery (revive point)
- **Run:** /spirit setcemetery at the desired location.
- Policy is controlled by respawnPolicy:
- same_world (default) → cemetery used only if in the same world as death.
- always_cemetery → always respawn at the cemetery.
- Mark a Spirit Healer
- Sneak + right-click an entity with the configured item (default: WOOD_SPADE).
- Or spawn one: /spirit spawnhealer <giant|golem|guardian|villager|polar_bear> [Name…]
- Remove mark on a healer by sneaking with the item again or /spirit removehealer while looking at it.

# Test the Flow
- Die, respawn as a ghost, follow the action bar/boss bar to the tomb or the healer.
- Near your corpse (within 10 blocks), left/right click anywhere to revive.
- At a Healer, right-click to revive (with configurable costs).

# Player Experience

# Ghost State**
- **Movement:** Flight enabled; noclip-like behavior; safe world clamping.
- **Visuals:** INVISIBILITY (hide body), GLOWING outline, NIGHT_VISION “milky” hue (auto-refreshed).
- **Audio:** Optional ambient loop using resource-pack sound key or vanilla fallback.
- **Protection:** Ghosts cannot be damaged or pick up items.

# Wayfinding
- **Action Bar:** Directional target name + distance.
- **Boss Bar:** Configurable title, color, segmented style, distance progress.
- **Breadcrumbs:** Particle trail steps from player toward the current target.
- **Target Choice:** wayfinding.prefer = healer_only | cemetery_only | healer_then_cemetery.

# On-Screen Guidance
- **Ghost Whisper (random):** Large center title every N seconds with helpful text.
- Revive Prompts (persistent while in range):
- Near corpse (≤ 10 blocks): “You can revive here — left or right click anywhere.”
- Near healer (≤ configurable range): “You can revive at the Spirit Healer — right-click the healer.”

# Revival Options
- **Near Death Point** (failsafe): Click within 10 blocks; optionally break nearby gravestone/tomb blocks before reviving so drops spill.
- **Spirit Healer:** Right-click to revive with costs that can scale over a time window.

# Features (Highlights)
- Healer NPCs
- Mark any living entity as a Spirit Healer (sneak + right-click with item).
- Optional spawn helper command; auto-naming & glow; villagers set to PRIEST/CLERIC.
- Gentle Roam: Randomized pacing within a 5-block leash around center (cemetery by default).
- Repel Field: Periodic pushback of mobs/animals/players (configurable targets), with optional “hard ring” snap near the boundary.

# Costs & Scaling
- Flat cost for /spirit res (XP or money).
- Healer scaling within a time window (scalingCosts.*):
- XP and/or money ramps per recent res (caps supported).
- Optional durability damage to armor (and hands) starting at a threshold res count.
- Vault is only required for money mode; XP mode works standalone.

# Resource Pack Mini-Server
- Serves a compact zip with: ghost loop, healer voice line, and pack metadata.
- Allows external file overrides on disk, or uses embedded assets.
- Auto-push prompt + friendly hints if players block server resource packs.

# Compatibility Shims
- Back-compat public methods (isGhostPublic, getGhostData, resurrectAtPublic) to integrate with older helper classes (e.g., RescueNearDeath).

# Commands
- /spirit res — Revive at cemetery (observes cooldown/cost).
- /spirit status — Show ghost status and nearest healer/cemetery distance.
- /spirit setcemetery — Set cemetery at your current position.
- /spirit clearcemetery — Clear the stored cemetery.
- /spirit spawnhealer <type> [Custom Name…] — Spawn and mark a Spirit Healer.
- /spirit removehealer — Unmark & remove the targeted healer entity.

# Aliases
- /ghost
- /reclaim

# Permissions
- spiritlinks.use
- Use basic features: /spirit res, /spirit status.
- Default: true

- spiritlinks.admin
- Admin actions: set/clear cemetery, spawn/remove healer.
- Default: op

- Optional Granular Nodes
- spiritlinks.markhealer — Toggle Spirit Healer with the shovel. (Default: op)
- spiritlinks.spawnhealer — Use /spirit spawnhealer. (Default: op)
- spiritlinks.removehealer — Use /spirit removehealer. (Default: op)

# Configuration (Key Sections)
- Respawn Policy
- respawnPolicy: "same_world" | "always_cemetery"
- Healer Marking
- healer.clickItem: WOOD_SPADE
- healer.requireSneakToMark: true
- healer.requireFunds: false

# Scaling Costs
- scalingCosts.windowSeconds: 900
- scalingCosts.xp.enabled/base/step/max
- scalingCosts.money.enabled/base/step/max
- scalingCosts.durability.enabled/triggerFromCount/damagePerPiece

# Ghost Visuals & Hue
- ghost.allowFlight: true
- ghost.useInvisibility: true
- ghost.reapplyHueEverySeconds: 30

# Effects & Breadcrumbs
- effects.nightVision: true
- effects.ghostParticles: true
- wayfinding.actionBar.enabled/everyTicks/format
- wayfinding.bossBar.enabled/color/style/maxDistance/title
- wayfinding.breadcrumb.enabled/everyTicks/particle/step/maxPoints

# Healer Movement & Repel
- healerRoam.enabled/center/radius/checkEveryTicks/maxYDrop
- healerRepel.enabled/radius/checkEveryTicks/baseStrength/verticalBoost/hardBoundary/hardBoundaryFactor
- healerRepel.affect.monsters/animals/villagers/golems/players

# Ghost Whispers & Revive Prompts
- ghostWhisper.enabled/minSeconds/maxSeconds/fadeIn/stay/fadeOut
- reviveHints.enabled/checkEveryTicks/fadeIn/stay/fadeOut/healerRange

# Near-Death Rescue (Click-to-Revive)
- rescue.enabled: true
- rescue.clickDistance: 10 (spherical; plugin enforces 10 blocks)
- rescue.breakTombs: true + rescue.tombBreakRadius: 2
- rescue.tombBlocks: [...] (best-effort material name matching on 1.12)
- rescue.captureDrops/giveItemsAtRevive/restoreXP: true

# Resource Pack Server
- resourcePack.enabled/host/port/path/publicHost/autoPushToPlayers
- resourcePack.externalGhostOgg/externalHealerOgg/externalPackPng
- music.enabled/volume/ghostLoopKey/healerClickKey/ghostLoopEveryTicks

# How to Use (Players)
- After Death
- You respawn as a ghost (glow outline + night vision).
- Follow the action bar/boss bar to your corpse or the nearest Spirit Healer.
- Random whispers remind you what to do.

# Reviving
- At Corpse: Walk within 10 blocks of your death spot, then left or right click anywhere.
- At Healer: Right-click the Spirit Healer. Costs may apply (see server rules).
- Items/XP can be restored at revive if the server enabled those options.

# Admin Tips
- Place healers at cemeteries or hubs; roaming is automatically leashed to the center.
- Use repel fields to keep hostile mobs from spawn hubs.
- If clients don’t receive the resource-pack prompt, see messages.packHint* guidance and confirm publicHost points to an address reachable by players.

# Building From Source
- Maven
- mvn clean package
- Requires Java 8; depends on spigot-api 1.12.2-R0.1-SNAPSHOT and optional VaultAPI 1.7 (scope provided).

# Known Limitations
- Designed specifically for 1.12.2; relies on older Bukkit API names (e.g., Material constants, no BlockData).
- CatServer/Forge mod blocks are matched by material name heuristics; not all mod gravestones will be detected.

# License
- MIT

#Credits
- Author: Luc Bellefeuille

Thanks to the Bukkit/Spigot and Vault communities.
