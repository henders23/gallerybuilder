# Gallery Builder

Design a walkable 3D gallery in the browser, walk through it, and export it as a single HTML file.

Gallery Builder is a rebuild of the
[Health & Life Promenade](https://github.com/henders23/health-and-life-gallery). It keeps the Promenade's
three.js renderer, materials, lighting, walking and visitor sheets, and adds a design layer in front of it,
so anyone can lay out their own gallery.

Designed and built by Paul Hendrie.

> **Trial version.** Gallery Builder is a trial, for experimentation purposes only.

## Files

| File | What it is |
| --- | --- |
| `index.html` | The app: the designer (start screen), the 3D walk-through engine, and the exporter. |
| `promenade.html` | The original Health & Life Promenade, unchanged. |
| `mesmerize-kevin-macleod.mp3` | Background music used only by the original Promenade: “Mesmerize” by Kevin MacLeod (incompetech.com), licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Gallery Builder itself has no music. |

It's a static site with no build step. Serve the folder with any static host (Vercel, GitHub Pages,
`python3 -m http.server`) and open `index.html`.

## The designer

- **Start screen.** Start from **The Dack Gallery**, a fully editable, downloadable 3D gallery (an entrance
  hall, a long gallery, a rotunda, a sculpture court and a quiet room, all of which can be changed or added
  to), start from a blank site, or open a saved design. The site is 300 × 300 m. The start screen opens every
  time the app does; close it to carry on with the design saved in this browser.
- **Rooms.** Draw square or round rooms, drag them into place and resize them with the handles. Each room
  has its own name and route number, ceiling height, floor (oak parquet, flagstone, marble, concrete, or
  carpet in eight colours), wall colour, lighting mood, accent colour and placard text.
- **Walls and doorways.** Rooms that touch share a wall. A new room drawn against another one gets a doorway
  automatically. You can also open or close doorways with the Doorway tool, and draw free-standing walls,
  either full height or low.
- **Exhibits.** The **Add an exhibit** button at the top of the right-hand panel adds a picture, a written
  piece or an object on a plinth. Describe it, then click the spot on a wall (or, for a plinth, the floor)
  where it should go — or let it hang itself in a room you choose. Works on the walls show as gold ticks on
  the plan: drag one to move it to any room wall, round-room drum or full-height free-standing wall. Pinned
  works stay put and the others arrange themselves around them, clear of doorways and signs. The
  **All exhibits** tab lists every work room by room, with search, so you can edit titles, text and pictures
  in one place.
- **Signs.** Wall signs come as a text panel, a banner with an arrow, the gallery title, a floor plan, or a
  visitors' wall. There are also standing signs, and every doorway gets a sign above it that you can
  reword.
- **Furnishing.** Carpets (rugs in four patterns), benches, plants, plinths with objects in glass cases, a
  welcome lectern, and the visitors' starting point.
- **Undo and redo, autosave, and a design check.** The design check flags overlapping rooms, rooms nobody
  can reach, and pictures that don't fit on the walls.

## Where your work is stored

Everything — rooms, signs, exhibits and the pictures you upload — lives in a single design. Nothing is uploaded
to a server: the Vercel site only serves the app.

- **In your browser.** The design saves itself to this browser's local storage as you go, so it's there when
  you come back on the same computer and browser. Pictures are shrunk to at most 1600 px and stored inside the
  design. Browsers allow only a few megabytes here, so a design with many pictures may be too big to autosave;
  the top bar says so when that happens.
- **In a file.** **File → Save design file** downloads the design as `.json`, and **Export HTML** downloads the
  walkable gallery with the design inside it. Either one can be opened again with **File → Open**, on any
  computer. These files are the only way to keep a copy or move a design elsewhere.
- **Works added while walking.** In Walk-through mode, the **Add work** sheet saves into your design too.
  In an exported gallery, a visitor's additions last only for their visit.

## Export

**Export HTML** downloads one self-contained page. The design, including your uploaded pictures, is
embedded in it. It needs an internet connection, because three.js loads from a CDN. **File → Open** reads an exported page back into the
designer, so you can keep editing it.

## How it fits together

`index.html` has three scripts:

- `layoutSrc`: the layout rules that turn a design into walls, doorways and hanging positions. The designer
  and the engine both use them, so the plan matches the 3D build.
- `engineSrc`: the walk-through engine, adapted from the Promenade.
- `builderSrc`: the designer.

An export copies the viewer's markup and styles, `layoutSrc` and `engineSrc`, together with the design as
JSON.
