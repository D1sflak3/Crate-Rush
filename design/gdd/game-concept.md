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

## Added by Shah on 2026-11-11 (third pass: tactics)
Brief: the mode felt like "you just keep dying and there's no strategy". Changes asked for:
- Smarter computer players.
- Every player picks an operator at the start (first called a role), in a dark room where each operator's
  kit is laid out with space between them. Clicking a kit lights it, moves the camera in and shows the
  operator's name, description and kit. 30 seconds to choose.
- Everything is bought: drones, ammo, revives, and all the old misc items, which are no longer free.
- One free revive each per match. After that you buy one, or a teammate uses a Revive Kit on you.
- Anything bought is held on a belt and can be handed to a teammate.
- A bigger, longer, more strategic map with more angles, detail and things in it; better graphics.
- A richer ground: it was the largest surface on the map and read as empty and smooth.

How it was built:
- Operators: Assault, Medic, Recon, Engineer, Heavy. Each has a starting kit and perks. Computer players
  take whichever operators nobody on their side chose.
- Money: Defenders start with $800, Raiders with $1,100 (the Defenders have the home ground). $300 an
  elimination, $100 an assist, $100 wage every 30 s while you are up, $100 for breaking an enemy gadget,
  $100 for reviving a teammate on the spot. Raiders also earn $200 each for finding the package before the
  first signal ping and $150 each the first time two of them lift it.
- Shop: 17 items. Belt of six kinds. G uses, Z/X cycle, 4 to 9 pick, H hands the selected item over.
- Ammo: a reload draws on a reserve; an Ammo Box adds three magazines a gun.
- Going down: no timed respawn. Free revive (once), then $500, or a teammate's Revive Kit: beside the
  body gets you up where you fell, from anywhere sends you back to base. A side with nobody up and nobody
  on the way back loses after 12 seconds.
- Gadgets: Recon Drone (you fly it; marks enemies it sees through walls), Spy Camera, Proximity Mine. All
  can be shot. Red fuel barrels around the port explode and chain.
- Timing: 45 s hide phase, 5:00 raid, first signal ping at 1:00 and then every 50 s.
- Map: 220 x 192 m. A rail yard behind the warehouses, a fuel depot with a pipe bridge to the south, a
  catwalk over the main road, a watchtower by the pad, a platform on the east stacks, 22 hiding places.
- Computer players: Defenders hold posts (two close, one on overwatch, one forward) and are not drawn off
  them; they hide the package a long haul from the ship. Raiders sweep hiding places as a squad, gather
  out of sight before a push, regroup when a push breaks, and escort a haul ahead and behind.

Balance, from all-computer matches on the final rules: Raiders won 19 of 36. Matches with a real player
in them have not been measured.

