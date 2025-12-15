![SpiritLinks Logo](https://github.com/lucbellefeuille/SpiritLinks/blob/main/spiritlinks_bottom_400.png)

# SpiritLinks (Mod)
**MMO-style “ghost run” death flow for Minecraft 1.12.2 (Forge).**  
Die → become a ghost → follow a clear death marker back → revive safely.

> **Versioning note (important):**
> - **v1.0.0 = Spigot plugin (legacy)**  
> - **v1.1.0 and later = Forge mod** (this README is for the **MOD**)

---

## Why SpiritLinks?
I wanted a death system that feels closer to an MMO:
- Death should be a **recoverable journey**, not a permanent gear/XP loss.
- No more losing your run to lava/despawn timers or chaotic recovery.
- A consistent way for players to **return to safety when revived** and keep death/revive behavior centralized and predictable.

SpiritLinks focuses on turning death into a guided “ghost run” where the player is clearly directed back to their death location and can recover without the usual Minecraft death frustration.

---

## What it does
When you die:
- You respawn as a **ghost** (visual effects + ghost-like movement).
- A **death marker** shows you where you died (designed to stay readable from far away).
- You follow the marker back and **revive** once you reach the correct location.

The goal is simple: **death becomes a guided recovery loop**, not a punishment spiral.

---

## Supported platforms / requirements (MOD)
- **Minecraft:** 1.12.2
- **Mod loader:** Forge (1.12.2)
- **Java:** Java 8 (1.8)
- **Singleplayer:** Supported
- **Multiplayer:** Supported on Forge servers (clients must have the mod too)

> Looking for the old Spigot/Bukkit server plugin? That’s **SpiritLinks v1.0.0** (plugin).  
> Everything **after v1.0.0** is the **Forge mod**.

---

## Installation (Forge Mod)
### Client (singleplayer / to join a modded server)
1. Install **Minecraft Forge 1.12.2**
2. Download the SpiritLinks **mod** `.jar` from the Releases page
3. Put it in:
   - `minecraft/mods/`
4. Launch Minecraft

### Dedicated server (Forge)
1. Set up a **Forge 1.12.2** server
2. Put the SpiritLinks **mod** `.jar` in:
   - `server/mods/`
3. Restart the server
4. Make sure players use the **same mod version** on their clients

---

## How to play
### After death
- You enter **ghost mode**.
- The mod displays a **death marker** to guide you back to where you died.

### Revival
- Follow the marker until you reach your death location.
- Revive (exact interaction depends on version/config — see below).

---

## Quick start (admin)
### 1) Set a cemetery (revive hub)
Stand where you want the revive point, then:
- `/spirit setcemetery`

Control how it’s used with:
- `respawnPolicy: same_world` (default) → cemetery used only if death was in same world  
- `respawnPolicy: always_cemetery` → always use the cemetery

### 2) Create a Spirit Healer
You can mark an existing entity:
- **Sneak + right-click** the entity with the configured item (default: `WOOD_SPADE`)

Or spawn one:
- `/spirit spawnhealer <giant|golem|guardian|villager|polar_bear> [Name…]`

Remove/unmark:
- Sneak + right-click again with the item, or
- `/spirit removehealer` while looking at it

### 3) Test the flow
- Die → respawn as a ghost
- Follow the **action bar / boss bar / breadcrumbs**
- Revive:
  - Near corpse (≤ 10 blocks): **left/right click anywhere**
  - At healer: **right-click the healer** (costs optional)

---

## Player experience
### Ghost state
- **Movement:** Flight enabled; noclip-like behavior; safe world clamping
- **Visuals:** INVISIBILITY, GLOWING outline, NIGHT_VISION “milky” hue (auto-refreshed)
- **Audio:** Optional ambient ghost loop
- **Protection:** Ghosts can’t be damaged and can’t pick up items

### Wayfinding
- **Action Bar:** Target name + distance + direction guidance
- **Boss Bar:** Configurable title, color, segmented style, and distance progress
- **Breadcrumbs:** Particle trail stepping toward the current target
- **Target selection:**  
  `wayfinding.prefer = healer_only | cemetery_only | healer_then_cemetery`

### On-screen guidance
- **Ghost whispers:** Random center-screen titles every N seconds
- **Revive prompts:** Persist while in range
  - Near corpse: “You can revive here — left or right click anywhere.”
  - Near healer: “You can revive at the Spirit Healer — right-click the healer.”

### Revival options
- **Near death point (failsafe):** Click within 10 blocks  
- **Spirit Healer:** Right-click to revive  
  Optional: XP cost and Durability loss and scaling within a time window

---

## Feature highlights
### Spirit Healers (NPCs)
- Mark almost any living entity as a healer
- Optional spawn helper command
- Auto-naming & glow
- Villagers set to PRIEST/CLERIC

### Gentle roam
- Random pacing within a small leash (default: around cemetery)

### Repel field (hub protection)
- Periodic pushback of mobs/animals/players (configurable targets)
- Optional “hard ring” snap near the boundary

### Costs & scaling (optional)
- Flat revive cost (XP or money)
- Scaling costs within `scalingCosts.windowSeconds`
- Optional durability damage to armor/hands after a threshold
- **Vault only required for money mode** (XP mode works standalone)

---

## Compatibility notes
- This is a **Forge mod**. It is **not** a Spigot/Bukkit plugin.
- If you run a Forge server, all players joining must have the mod installed (unless a specific version explicitly states otherwise).

---
