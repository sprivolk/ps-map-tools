# PlaceholderShooter map tools

Make maps for PlaceholderShooter in Blender, the way Hammer makes them for CS: boxes on a grid (brushes), tool materials
(clip, nodraw…), spawns and zones, then play the map in the game — on this computer, or on a phone.

Needs **Blender 5.2** or newer.

## Install and updates

1. Blender → **Edit → Preferences → Get Extensions**.
2. Top right: **Repositories ▾ → + → Add Remote Repository**, URL:
   `https://raw.githubusercontent.com/sprivolk/ps-map-tools/main/index.json`
   Tick **Check for Updates on Startup**.
3. Find **PlaceholderShooter map tools** in the list → **Install**.

Blender looks for a new version each time it starts: **Get Extensions → Update** (or update all). Restart Blender after
an update.

## A new map

**File → New → PlaceholderShooter map**: a name (letters, digits, `_`, as `de_dust2`) and a folder. You get a file with
the map's collections, a floor, a spawn a side, the grid and four views (top, front, side, 3D).

The tools are in the 3D view's sidebar (**N**), in their tabs: **Build**, **Object**, **Entities**, **View**, **Play**.

## Keys (Object Mode, in a map file)

| Key | |
|---|---|
| **Q** | the brush tools round the mouse |
| **Shift+Q** | materials |
| **F** | the selected's settings at the mouse |
| **[ ]** | the grid finer / coarser (1 to 256 units) |
| **Ctrl** while moving | off the grid |
| **F9** | the last tool's settings (size, turn…) |

A unit is CS's: 16 units = 0.4 m; a player is 72 units tall, 32 wide; a step at most 18; a jump onto 57 at most.

## Building

- **Draw brush**: drag a rectangle in a flat view (top, front, side), then drag its height in another. Enter: done.
- **Resize**: drag the yellow handles of the selected brushes in a flat view; they go along the grid.
- **Box**, **Snap** (corners onto the grid), **Square** (a crooked box made square), **Split** (a mesh into brushes).
- **Make a room**: the selected box becomes a hollow room (floor, walls, ceiling).
- **Door / Window**: select a wall (or a room), put the 3D cursor where the opening goes (Shift + right click on it),
  press it; F9 or the Object tab: width, height, from the floor, top Flat or **Arch**.
- **Hole**: the same in a floor or a ceiling.
- **Stairs**, **Arch** (an archway or a tunnel), **Cylinder**: at the 3D cursor, or filling the box selected.
- **Cut with a plane**: a brush in two, through the 3D cursor.

Stairs, arches, rooms, cylinders, walls with doors and floors with holes keep their settings: they open at the mouse
right after the tool (later: **F**, or the **Object** tab); change one, it is built again where it stands, and **Ctrl+Z**
takes back that one change (not the whole door). **Sizes on the grid** (on by default) keeps the sizes and offsets in
whole grid steps. Edited by hand in Edit Mode, or scaled, it becomes a plain brush.

**Materials** (Build tab or Shift+Q): **Colours** (just colours), **Surfaces** (what bullets go through and how steps
sound: concrete, metal, wood…), **Tools**: Player clip (invisible wall), Nodraw (a face not drawn), Grenade clip, Block
bullets, Kill zone, Ladder.

A brush is **Solid** (seen and walls players), **Detail** (seen, players go through), or **No collision**.

**The map's edge**: select the walls round the map, **Map edge** (Build → Brush tools): their outer side is not drawn
(Nodraw) and a player clip goes over them up to the map's **Ceiling** (0: the highest brush + 128 units) — nobody gets
over. A map closed all round this way is **sealed**, as in Source: at export the air is flooded from the spawns, and
every face turned only to the outside (the back of the edge walls, the ground past them, a floor's underside) is left
out, along with faces no player has in front of them (Play → *Leave out faces nobody sees*; mark a face *Always draw*
to keep it). Walls, Nodraw brushes and player clips close the map (a clip is seen through: what is behind it outside the map
shows the sky); details and glass do not.
A map not closed **leaks**: **Check the map** draws a red line from a spawn to where the air gets out; until it is
closed, the outside stays. It also says where players get to the very edge of the map, or on top of an edge wall.
Faces not drawn (Nodraw, left out) still stop the baked light.

Brushes may overlap: faces hidden inside other brushes are cut away at export. Two faces on top of each other in one
plane flicker in the game — **Check the map** finds them.

## Entities

**Entities** tab: Spawn T / CT, Bomb site A / B, Buy zone T / CT, Lamp, Sun, Kill zone, Ladder, radar markers — at the 3D
cursor. With a brush selected, Ladder and the zones turn that brush into them (drawn to the size wanted).

## Playing it

**Play** tab:

- **Check the map**: what is missing or wrong (no spawns, a spawn in a wall, flickering faces…), each with a button to
  go there.
- **Test and play**: the game on this computer starts on the map (or goes to it if it runs). Set the game first:
  Preferences → Add-ons → PlaceholderShooter map tools → **Game** (PlaceholderShooter.exe).
- **Bake Fast / Bake Final & play**: with light baked in Blender (Cycles: sun, lamps, bounced light). Final takes minutes.
- **On a phone** (no game on this computer): **Export .psmap** (or **Bake Final & export .psmap**) — `<map>.psmap` beside
  the `.blend`. Send it to the phone; in the game: **Workshop → Resources → Import map…**, then Play.

If the game says the map is of a newer format, update the game.
