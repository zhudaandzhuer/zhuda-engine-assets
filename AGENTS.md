# For agents: finding and fetching an asset

This repository is about 4 GB of pictures. Do not clone it to find one file.

## The three requests

1. `catalog/kinds.json`: every kind of asset, what it is for, how many there are and in what state.
2. `catalog/<kind>.json`: the assets of that kind (no prompts; small enough to read).
3. `baseUrl + path` of the entry you chose.

```sh
BASE=https://raw.githubusercontent.com/zhudaandzhuer/zhuda-engine-assets/main
curl -s $BASE/catalog/kinds.json
curl -s $BASE/catalog/prop.json
curl -sO $BASE/3d/props/ancient-altar-table-candlesticks.png
```

`catalog.json` is every slice in one file, with the prompt of each picture that has one (about 1 MB).

## An entry

| Field | Meaning |
| --- | --- |
| `id` | the path without its extension; unique |
| `kind`, `medium` | what it is (`prop`, `material`, `ui`, …) and where it is used: `2d`, `3d-reference` (a picture to turn into a model) or `texture` |
| `style` | `ancient`, `ruin`, `toon`, `painted`, `scifi`, `fantasy`, `city`, or null when it has none |
| `path` | the file; its address is `baseUrl + path` |
| `width`, `height`, `bytes`, `alpha`, `sha256` | of that file. `alpha` is true when some pixel is transparent |
| `background` | `transparent`, `black` (meant for additive blending) or `opaque` |
| `repeat`, `seam` | whether it tiles (`both`, `x`, `y`, `none`) and whether its edges were made to meet (`closed`) or are as generated (`raw`) |
| `status`, `issues` | see below |
| `files` | a material's files: `albedo`, `height`, and where made `normal`, `albedo-512`, `height-512`, `normal-512` |
| `cells` | the pieces a sheet was cut into (icons, faces, pickups), as paths |
| `view` | `front`, `back` or `side` for a reference picture |
| `prompt` | what the picture was asked to be (second batch only, in `catalog.json`) |

## Status

- `ok`: fits what was asked, by measurement and a look at thumbnails. No person has looked at it closely.
- `flagged`: usable, with the issue stated in `issues`.
- `raw`: as generated; a step of post-processing is still owed and `issues` says which.
- `redo`: wrong. Do not use it.

Take `ok` first. Read `issues` before taking a `flagged` one.

## Pictures for an image-to-3D step

- `prop`: one object, transparent background, no outline. Most are a front view; vehicles are a side view.
- `character-ref`: `<name>-front.png` and `<name>-back.png`, the same pose and size.
- `creature-ref`: `<name>-side.png` and `<name>-front.png`.

None has been turned into a model yet; there is no `.glb` here.

## Materials

`textures/materials/<name>/albedo.png` (sRGB colour), `height.png` (grey, white is high), `normal.png` (tangent space,
OpenGL convention: green up). The ones with `seam: "closed"` tile; the ones with `status: "raw"` do not yet and have no
normal map.

## What is not promised

Nothing here was accepted by a person one picture at a time. A path stays where it is once published; a picture marked
`redo` may be replaced under the same path, and its `sha256` will change with it. The catalog is written by a script on
the owner's machine: do not edit it by hand, and do not add files here without it.
