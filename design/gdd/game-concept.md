# Game Concept: Blackout (Showdown mode) on Blackwater Port

Source: Shah's brief, 2026-11-10. This covers one new Showdown mode and its map, not the whole of Crate Rush.

## Pitch
A 4v4 heist on a storm-dark container port. A sealed package is craned onto the dock in an opening cutscene.
The Defenders hide and guard it. The Raiders come off their cargo ship, find it, and haul it back aboard.

## What the player feels
Defender: the tension of choosing a hiding place and holding it. Raider: the hunt, then a slow, exposed carry home.

## Core mechanics
- Two teams of four: Raiders and Defenders.
- The package is a large box. It takes two players to carry, they move at 0.5x speed, and they cannot use weapons while carrying.
- Carrying works like "carry the glass": one player on each end, moving together.
- Defenders may hide the package anywhere on the map.
- Raiders win by getting the package onto their cargo ship. Defenders win if time runs out first.

## Core loop
Cutscene (package delivered) -> hide phase (Defenders only) -> raid (find, fight, carry) -> one side wins.

## Map
Blackwater Port, modelled on the reference picture: container stacks, two yellow portal cranes, corrugated sheds,
a blue fenced yard, a raised walkway with stairs, the sea along one side with the Raiders' ship moored at the quay.

## Menu
A dark, mysterious custom banner for the mode on the game modes tab.

## MVP
Everything above, playable solo with computer-controlled teammates and opponents.

## Technical considerations
Single-file browser game (Three.js r160). Party play is leader-hosted; syncing the package over the party
netcode is out of the MVP.

## Added by Shah on 2026-11-10 (second pass)
- The map is much bigger, with full-size containers the package fits into many times over.
- Raiders look like black-ops agents in black gear; Defenders wear navy with bulkier gear.
- In plain Blackout your guns are cosmetic only. A second variant, Blackout Rumble, lets them work normally.
- A mid-match shop sells gear; money comes from kills, as in Rainbow Six Siege or CS:GO.
- Low sun, storm clouds, stronger shadows and lighting, after the reference picture.
- Settings: move and resize the phone buttons; rebind controller buttons.
