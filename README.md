# Roblox Combat RPG

> Proprietary Roblox combat project built with Luau

A modular, server-authoritative R6 combat system featuring
entity state machines, persistent player data, projectile
simulation, hit detection, character customization, and
physics-based character systems.

**Source code:** Private

## Demonstration

[Watch Gameplay / Technical Demonstration](YOUR_VIDEO_LINK)

## Technical Highlights

- Server-authoritative combat architecture
- Entity-based state machines for players and NPCs
- Modular client/server architecture
- Persistent player data using ProfileService
- Server-side melee hit detection
- Projectile simulation using SecureCast
- Data-driven weapon and character customization
- Ragdoll and physics systems using SmartBone
- Modular resource and connection management

- ## Architecture

The project follows a modular `MainServer / MainClient / MainPlayer`
architecture with separate managers, handlers, entity profiles,
state machines, and shared utilities.

                         COMBAT ARENA
                              │
             ┌────────────────┴────────────────┐
             │                                 │
         SERVER                              CLIENT
             │                                 │
       MainServer                          MainPlayer
             │                                 │
      ┌──────┼──────┐                  ┌───────┼───────┐
      │      │      │                  │       │       │
  Managers Handlers States          Input   Effects    UI
      │      │      │
      │      │      ├── Player
      │      │      └── Dummy
      │      │
      │      ├── Combat
      │      ├── Player
      │      └── Dummy
      │
      ├── EntityManager
      ├── DataManager
      ├── CombatManager
      └── CollisionManager

## Combat State Machine

Combat is built around explicit entity states rather than a
single monolithic combat script.

### Player States

- Idle
- Attacking
- Blocking
- Parrying
- Dashing
- Weapon Drawn
- Stunned
- Posture Broken
- Unconscious
- Dying

Each state contains its own behavior and transition logic,
allowing combat mechanics to be developed independently.

              Idle
               │
       ┌───────┼────────┐
       ▼       ▼        ▼
   Attacking Blocking  Dashing
       │       │
       ▼       ▼
   Parrying  Posture
                │
                ▼
             Stunned
                │
                ▼
           Unconscious
                │
                ▼
              Dying

## Client / Server Architecture

The client is responsible primarily for input, presentation,
and local prediction, while the server maintains authoritative
gameplay state.

### Client

- Input handling
- Local visual effects
- UI updates
- Rendering
- Client-side state prediction

### Server

- Combat validation
- Damage
- Hit registration
- Entity state
- Player data
- Gameplay decisions

Client
  │
  │ RemoteEvent
  ▼
CharacterHandler
  │
  ▼
CombatHandler
  │
  ▼
State Machine
  │
  ▼
CombatManager
  │
  ▼
Server Result

## Data & Persistence

Player persistence is separated from gameplay logic through a
dedicated DataManager.

Player
  ↓
PlayerHandler
  ↓
DataManager
  ↓
ProfileService
  ↓
Persistent Profile

## Data-Driven Systems

Game content is separated from the systems that process it.

- WeaponData
- RaceData
- AccessoryData
- HairData
- UniformData
- CombatSettings
- AnimationData
- SoundData

This allows new content to be added through configuration
without modifying the underlying systems.

```Luau
local module = {}

function module.Start(ModulesCache)

	return {
		Attack = {
			Counterable = true,
			Parryable = true,
			Blockable = true,	
			Evadeable = true,

			Endlag = 0.25,
			Damage = 8,

			BlockDamage = 17,
			ParryDamage = 20,

			TrueStun = 0.1,
			SoftStun = 0.3,

			HitEffects = {
				"Blunt";
			},
			HitTypes = {
				M1 = true;
			},
			Properties = {
				Range = 6.5,
				Width = 7,
				Height = 11,
				Length = 0,
			},
		};
		Critical = {
			Counterable = true,
			Parryable = true,
			Blockable = true,	
			Evadeable = true,

			Endlag = 0,
			Damage = 11,

			BlockDamage = 17,
			ParryDamage = 20,

			TrueStun = 0.1,
			SoftStun = 0.3,

			HitEffects = {
				"Blunt";
			},
			HitTypes = {
				Critical = true;
			},
			Properties = {
				Range = 6.5,
				Width = 7,
				Height = 11,
				Length = 0,
			},
		};
	}
end

return module
```
## Technologies

### Core
Note: Third-party libraries are integrated into the project's architecture and are not presented as original implementations.

- Luau
- Roblox Studio
- Roblox Engine APIs
- RemoteEvents
- ModuleScripts

### Libraries

- ProfileService — persistent player data
- SecureCast — projectile simulation
- SmartBone — bone physics
- Iris — development/debug UI

## Source Code

The complete source code is private because this is a proprietary
project.

This repository instead provides:

- Architecture documentation
- Technical diagrams
- System explanations
- Demonstrations
- Selected standalone examples

The project's implementation can be discussed in greater detail
during an interview or technical review.

## Screenshots

### Combat
