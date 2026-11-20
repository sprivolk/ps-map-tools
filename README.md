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
- **Resize**: drag the yellow handles of the selected brushes in a flat view; they go along the grid. A room or a wall
  with openings sizes the same way: its sides move its walls, the doors and windows stay where they are. Straight
  stairs too: taller, more steps (each as high as before, 18 units at most), longer, deeper steps (their number: F). Its doors and
  windows show cyan frames (in the views facing their wall; from above, along it): drag inside one to move it, its edge
  to size it. Holes in floors and ceilings have the same frames: from above both ways, from the side along the floor.
  **V** in Resize: the edges (Hammer's vertex tool) — white squares on the brush's corners; drag one in a flat view
  and the edge behind it moves along the grid: a slanted side (a wall slanted on one side only, a parallelogram), or
  onto another corner, a wedge. Not where the brush would get a dent. V again: the sides. Plain brushes only (a room:
  Split into brushes first).
- **Box**, **Snap** (corners onto the grid), **Square** (a crooked box made square), **Split** (a mesh into brushes).
- **Make a room**: the selected box becomes a hollow room (floor, walls, ceiling), one object keeping its settings (the
  export makes it brushes). **Split into brushes** (Object tab): its floor, ceiling and four walls as objects of their
  own, the walls keeping their doors and windows, the floor and ceiling their holes — each moved or resized apart.
- **Door / Window**: select a wall (or a room), put the 3D cursor where the opening goes (Shift + right click on it),
  press it; F9 or the Object tab: width, height, from the floor, top Flat or **Arch**.
- **Hole**: the same in a floor or a ceiling (a room's too: the cursor on its floor or its ceiling).
- **Stairs**, **Arch** (an archway or a tunnel), **Cylinder**: at the 3D cursor, or filling the box selected.
- **Cut with a plane**: a brush in two, through the 3D cursor.
- **Cut through** (a way through a slanted wall, a tunnel's end): make a brush of the hole's shape (Box, Arch,
  Cylinder) going right through the wall, select the wall (or several brushes), then the cutter last (Shift + click),
  press it (Brush tools, Q or the Object tab). The cutter becomes a wire, not exported: move it (G) or **Resize** it and
  the hole follows; its material is the hole's sides. A room or a wall keeps its settings under the cut. Deleted, the
  hole closes. **Apply cut** makes the hole for good (the cutter goes; a room or a wall becomes a plain brush). View →
  **Cutters** shows or hides them.

Stairs, arches, rooms, cylinders, walls with doors and floors with holes keep their settings: they open at the mouse
right after the tool (later: **F**, or the **Object** tab); change one, it is built again where it stands, and **Ctrl+Z**
takes back that one change (not the whole door). **Sizes on the grid** (on by default) keeps the sizes and offsets in
whole grid steps. Edited by hand in Edit Mode, or scaled, it becomes a plain brush. A wall with openings made plain so (its pieces round the holes) becomes one again with **Wall with
openings again** (Object tab): its holes are found between the pieces.

**Materials** (Build tab or Shift+Q): **Colours** (just colours), **Surfaces** (what bullets go through and how steps
sound: concrete, metal, wood…), **Tools**: Player clip (invisible wall), Nodraw (a face not drawn), Grenade clip, Block
bullets, Kill zone, Ladder.

**The Art tab** (dressing the map once it plays well): **Group** — the groups as in Build, and the solo button on a group's row starts **working in it**: only it in the views, selected, in sight (Stop: everything back). **Materials** — the art library as pictures (Columns / Size under them); a picture puts its material on the selected brushes (in Edit Mode: the selected faces) and makes it the current one; **Pick** (eyedropper) takes the material of a face clicked in the view as the current one, **Put** puts the current one.

**Faces** (Art tab): Hammer's face edit on the selected faces (in Object Mode: all faces of the selected brushes) — the texture moved by the grid step (arrows), turned 90°, ×2 / ÷2, **Fit** (the picture once over the face), **Fit ↔** (once across), **Copy active face**, **Reset**. Kept in face attributes (ps_tex_off, ps_tex_scale, ps_tex_rot) the world UVs are made through, so they stay when the brush moves; a mirror copy takes them (a maker's brush, built again, loses them). **Patchwork**: **Cut into sheets** (Edit Mode: the selected faces cut on the world grid of 1.2 × 2.4 m sheets, the textures' seams), a **mix** list (Add the current material; the first one is the main), **Mix** (the mix over the selected faces at random; F9: seed, how many keep the first), **Shuffle sheets** (each face's texture shifted by whole sheets and turned round at random).

**Art materials** (Art tab): the map's real look, from a shared library — `ArtSource/Materials/<name>/` (another folder: the add-on's preferences), a folder per material with its colour picture and `material.json` (`{"surface": "plaster", "size": 2.0}`: what bullets and steps meet, how many metres the picture covers). **New from picture** copies a picture in (a downloaded set's `_Color` picture: the rest is left, the game draws colour only). A button puts it on the selected brushes (in Edit Mode: on the selected faces); it lies by the world like the Dev textures, the same size on every brush, so walls meet without seams. **⇄** puts it instead of the active object's active material on all the selected (a group selected: Dev Plaster → the house's plaster everywhere). The active art material's size and surface are set below the list and kept in the library; **Look again** brings the file's art materials up to the library (a picture painted over).

**Groups** (Build tab): **Into a group** names the selected objects (the house); each group's row selects it (Shift: adds), shows only it in every view (pressed again: all back) or renames it. The objects stay in their collections: the export and the mirror are as before.

**Trims** (Art tab): a profile along a line — beams, planks, skirtings, door frames, pipes, rails. In Edit Mode (edge select) pick edges, on one brush or several: **Trim from selected edges** makes one trim; edges meeting end to end become one line, the corners mitred (a frame round a door is one piece). Its settings, live: profile (**Box** width × height, **Round**, **Angle**), shift across / up, joints (Mitre / Overlap), Solid (else Detail: seen only), the material (the eyedropper button: the current one). Its own UVs run along it: the grain follows the beam on any picture. **Edit path**: the line as points (G move, E add, X remove), the trim follows; Done. **Release**: a plain brush from then on. A straight staircase selected: **Stringer** (a sloped board on each open side) and **Railing** (a handrail and posts): they follow the staircase when it changes.

**Props and decals** (Art tab): **props** from ArtSource/Props/<name>.blend (the first mesh; <name>.png beside it is its picture; **Add to library** writes the active mesh there, its origin the point it stands on). **Place** (a prop's button): it follows the mouse over the surfaces standing on them — R / Shift+R turn, + / − size, Ctrl the grid, click puts it and goes on, Esc stops; a prop is a model (copies share its mesh). **Scatter** (Edit Mode, faces selected): that many at random over them, turned and sized at random. **Decals** from ArtSource/Decals/<name>/<name>.png (transparency cuts them out) + decal.json (its size); **New decal** adds a PNG; placed the same way, a flat Detail brush a hair off the face, baked as the walls.

**Prefabs** (Art → Group): **Make <group> a prefab** — its objects stay where they are, the first copy; **Place copy** puts a linked copy at the 3D cursor (move it with G, turn it with R Z): change the group and every copy changes. **Make real**: a copy as objects of its own. The export makes every copy real first.

**Grain pairs**: a library material with a twin named `<name>_Vertical` (the same picture turned upright: House_Beam) is one button; put on a brush, each face gets the one whose grain runs along the brush's longest side. Beams, posts and boards are drawn by hand as box brushes (make them Detail if players should pass) and get the grain right at once.

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

### Symmetric maps (Build → Mirror)
Deathmatch and quick-mode maps are often symmetric. Choose the symmetry: **Mirror X** (left and right swap), **Mirror Y**
(front and back swap) or **Turn 180°** (whichever side one plays, the same map), and the **Centre** — an empty outside the
map (made at 0, 0 the first time; the cursor button puts it at the 3D cursor), its line drawn in the views. Build one half,
select what is done and press **Copy to the other half**: each copy is placed through the centre (brushes mirrored with
their faces outward, spawns looking the mirrored way, a door's hinges and side where the mirror puts them), T and CT
swapped. A copy stays **linked**: it follows every move, reshape and setting of its original (and the centre's moves);
moved by hand, it goes back. **Unlink** lets a copy be changed on its own; **Reset and link** puts it back where the
symmetry has it, as its original is, and links it again. **Select the other half** swaps the selection to the partners.

## Entities

**Entities** tab: Spawn T / CT, Bomb site A / B, Buy zone T / CT, Lamp, Sun, Kill zone, Ladder, radar markers — at the 3D
cursor. With a brush selected, Ladder and the zones turn that brush into them (drawn to the size wanted).

**The sun**: its arrow is where the light goes — turn it with **R** (where it stands does not matter, only its way);
the Object tab says how far down and toward where. **Preview sun** (View tab, or the Object tab) puts a Blender sun on
its arrow: the views (Material Preview) show its shadows while you turn it. Not exported: the bake makes its own.

**Ambient zone** (Entities; a brush selected becomes one): a volume whose dark places the bake lifts a little — walls,
floors and the probes players are lit by — so a dark room stays dark but players are seen. Only the dark: where a lamp
or the sun already lights it, hardly anything changes. Object tab: its **Color**, **Brightness** (how light its
darkest places get: 0.06 a dark room; more gets flat and grey) and **Fade** (units past its sides over which it
fades out, smoothly: no seam; within it, all of it — walls as lit as players). Baked light only (Bake Fast / Final).

## Models

A mesh made elsewhere (a plant, a pot, a staircase from a library) goes on the map as a **model**: select it, Object
tab → **Make model**. It moves into the map's **Models** collection and stays as it is — its own UVs, materials and
smoothing; its modifiers and particles (a plant's leaves) applied at export — lit by the probes as players are (not
baked). A model does not collide itself: a **collision box** (the Collision tool: invisible, stops players and bullets,
its surface the bullets meet) is made round it, parented to it — it moves and turns with the model; Resize trims it,
**Add collision box** adds more, deleting it leaves none. **Make brush again** turns it back. Check map warns of meshes
that are neither brushes nor models: the game leaves them out.

**Simplify** (a model's Object tab): fewer triangles — Blender's Decimate as its last modifier, applied at export, the
mesh itself kept. Auto goes by its size (about 1 500 triangles a metre: a chair a couple of thousand, not hundreds of
thousands); the **Keep** slider sets it, the tab shows the triangles before and after; X: as it was.

**Leaves as pictures** (a model's Object tab): its flat parts — the leaves its particles scatter, or the model itself
when flat (thinner than a 20th of its size) — drawn as **cards**: a square of two triangles with their picture seen from
above, transparent round it. The same look for a few hundredth of the triangles (a modelled leaf of 948 faces, thousands
on a plant). Seen in Blender at once; the originals are kept, hidden and left out of the export; the pictures are saved
in the map's `cards` folder and made once. Pressed again: the originals back. Check map tells when the models weigh more
than a phone draws smoothly (300 000 triangles), and which most.

**Pictures** (Play tab: 512 / 1024 / 2048): at export each material keeps only its colour picture (the game draws no
normal, roughness or height pictures), at most that size, and how it lies (a Mapping node's scale and offset); the
textures are drawn through the UV map Blender renders with.

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
