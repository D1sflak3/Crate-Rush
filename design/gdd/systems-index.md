# Systems Index: Blackout (first drafted as "Black Cargo")

Made with the map-systems workflow, run autonomous / solo review / terse. Director gates skipped (solo mode);
the `.claude/docs` gate and template files the skill refers to are not in this project, so the tables follow the
column contract quoted in the skill itself.

## Overview
Blackout is one new Showdown mode in two variants (Blackout, Blackout Rumble) plus one map. It reuses the existing shooter (movement, weapons, bots, HUD,
results) and adds an objective layer on top: a two-person package, three match phases, respawns and role-aware bots.
The package carry is the bottleneck: the phases, both win conditions, the bots and the HUD all read its state.
Assumptions made without asking (all are single constants to change): 40 s hide phase, 3:30 raid, respawns
(Raiders 8 s, Defenders 6 s), a signal ping that shows Raiders the package every 25 s, overtime while Raiders are
mid-carry, your side picked at random, solo only for now.

## Systems Enumeration

| # | Name | Category | Priority | Status | Design Doc | Depends On |
|---|------|----------|----------|--------|------------|------------|
| 1 | Mode registry entry (Blackout, 4v4, one map) | Core | MVP | Implemented | - | - |
| 2 | Blackwater Port map (layout, collision, climb routes, hide spots) | World | MVP | Implemented | - | 1 |
| 3 | Port look (storm sky, rain, sea, ship, cranes, lamps) | Presentation | MVP | Implemented | - | 2 |
| 4 | Roles and spawns (Raiders on the ship, Defenders on the dock) | Gameplay | MVP | Implemented | - | 1, 2 |
| 5 | Match phases (cutscene, hide, raid, overtime, end) | Gameplay | MVP | Implemented | - | 1, 4 |
| 6 | Package (state, pick up, drop, two-person carry link) | Gameplay | MVP | Implemented | - | 2 |
| 7 | Carry rules (0.5x speed, no weapons, no ladders or jumps) | Gameplay | MVP | Implemented | - | 6 |
| 8 | Win conditions (ship zone, timer) | Gameplay | MVP | Implemented | - | 5, 6 |
| 9 | Respawns (timed; replaced by 28) | Gameplay | MVP | Superseded | - | 4, 5 |
| 10 | Package visibility (Defenders always, Raiders by sight or ping) | Gameplay | MVP | Implemented | - | 6 |
| 11 | Bot objectives (hide, guard, search, help carry, haul, escort) | AI | MVP | Implemented | - | 6, 8, 10 |
| 12 | Delivery cutscene | Presentation | MVP | Implemented | - | 3, 5 |
| 13 | Mode HUD (roles, phase, package marker, grab prompt, respawn) | UI | MVP | Implemented | - | 5, 6, 9, 10 |
| 14 | Input (interact on keyboard, touch, controller) | UI | MVP | Implemented | - | 6 |
| 15 | Modes-tab banner | UI | MVP | Implemented | - | 1 |
| 16 | Results and rank points for the mode | Meta | MVP | Reused | - | 8 |
| 17 | Party sync for the package | Networking | Alpha | Not Started | - | 6, 5 |
| 19 | Variants: guns as looks only (Blackout) or full powers (Rumble) | Gameplay | MVP | Implemented | - | 1 |
| 20 | Gear shop and match money (eliminations, assists, wage) | Economy | MVP | Implemented | - | 5, 9 |
| 21 | Uniforms (black-ops Raiders, armoured navy Defenders) | Presentation | MVP | Implemented | - | 4 |
| 22 | Port lighting (low sun, storm-cloud sky, long shadows) | Presentation | MVP | Implemented | - | 3 |
| 23 | Phone button layout editor | UI | MVP | Implemented | - | - |
| 24 | Controller rebinding | UI | MVP | Implemented | - | - |
| 25 | Operators (five kits and perks) and the operator room | Gameplay | MVP | Implemented | - | 5, 20 |
| 26 | Belt: hold, select, use and hand over what you buy | Gameplay | MVP | Implemented | - | 20 |
| 27 | Ammo reserve and Ammo Boxes | Gameplay | MVP | Implemented | - | 20, 26 |
| 28 | Revives (one free, bought, Revive Kit) and the team-wipe rule; replaces 9 | Gameplay | MVP | Implemented | - | 5, 20, 26 |
| 29 | Gadgets: Recon Drone, Spy Camera, Proximity Mine, marks through walls | Gameplay | MVP | Implemented | - | 26 |
| 30 | Fuel barrels (shoot to explode, chain) | World | MVP | Implemented | - | 2 |
| 31 | Objective money for Raiders (found before the ping, first lift) | Economy | MVP | Implemented | - | 10, 20 |
| 32 | Tactical computer players (posts, squad sweep, rally, regroup, utility, revives, shopping) | AI | MVP | Implemented | - | 11, 20, 28, 29 |
| 33 | Map extension: rail yard, fuel depot, pipe bridge, catwalk, watchtower, platform | World | MVP | Implemented | - | 2 |
| 34 | Ground detail: shader wear and wet patches, decals, markings, clutter, rain rings | Presentation | MVP | Implemented | - | 3 |
| 35 | Lighting extras: lamp pools and shafts, mist, beacons, lighthouse beam | Presentation | MVP | Implemented | - | 22 |
| 18 | First-person carry hands, bot carry pose | Presentation | Full Vision | Not Started | - | 6 |

## Dependency Map
- Foundation: 1.
- Core: 2, 4, 6.
- Feature: 5, 7, 8, 9, 10, 11.
- Presentation: 3, 12, 13, 14, 15.
- Polish: 16, 17, 18.
- Bottleneck: 6 (seven systems depend on it). No circular dependencies.

## Priority Tiers

| Tier | Meaning |
|------|---------|
| MVP | Needed for one full solo match from cutscene to result |
| Alpha | Party play |
| Full Vision | Carry animation polish |

## Recommended Design Order

| Order | System | Priority | Layer | Agent(s) | Est. Effort |
|-------|--------|----------|-------|----------|-------------|
| 1 | Mode registry entry | MVP | Foundation | - | S |
| 2 | Blackwater Port map | MVP | Core | - | L |
| 3 | Package | MVP | Core | - | L |
| 4 | Roles and spawns | MVP | Core | - | S |
| 5 | Match phases, win conditions, respawns | MVP | Feature | - | M |
| 6 | Carry rules, package visibility | MVP | Feature | - | S |
| 7 | Bot objectives | MVP | Feature | - | L |
| 8 | Port look, cutscene | MVP | Presentation | - | L |
| 9 | HUD, input, banner | MVP | Presentation | - | M |
| 10 | Party sync | Alpha | Polish | - | L |

## High-Risk Systems
- Package carry link: two bodies tied together around corners and on stairs.
- Bot objectives: bots must finish a carry without a human, or matches stall.

## Progress Tracker
22 of 24 systems in place. Open: 17 (party sync), 18 (carry animation).
