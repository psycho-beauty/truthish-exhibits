# Truthish – Exhibit files

This repo feeds the **Exhibit A** hologram projector in the Truthish VRChat world.
The world loads files from `https://psycho-beauty.github.io/truthish-exhibits/` at show time,
so you can change exhibits without re-uploading the world.

## Slots

There are 24 slots. Each one can hold a 3D model, a photo, or both:

| File | What it is |
| --- | --- |
| `exhibit01.tsh` … `exhibit24.tsh` | **Encrypted** 3D model, made by `truthish_exhibit.py`. Shown as a spinning hologram. |
| `exhibit01.jpg` … `exhibit24.jpg` | For a `.tsh` model this is its texture, **scrambled**. On its own, it's shown as a plain photo. |
| `exhibit01.obj` … `exhibit24.obj` | Optional plain OBJ, only for models you're free to share (e.g. your own scans). |

- If a slot has none of these, the projector shows "SIGNAL LOST".
- `exhibit24` is a sample trophy (plain OBJ). `exhibit01` is an encrypted test model.
- Everything here is public, but `.tsh` models and their textures can only be decoded by the world.

## Adding exhibits (recommended): `truthish_exhibit.py`

The script lives in the world's Unity project at `Tools/truthish_exhibit.py`. Don't upload it here: it contains the decryption key.

```
python truthish_exhibit.py raccoon.fbx --slot 1        # any OBJ / FBX / glTF / GLB / Blend
python truthish_exhibit.py photo.jpg --slot 2          # photo-only exhibit
python truthish_exhibit.py --list                      # what's in each slot
python truthish_exhibit.py --clear --slot 3            # empty a slot
```

It converts the model, simplifies it to 20,000 triangles if needed (using Blender), merges its textures, encrypts it, uploads it here, and removes any plain OBJ left in that slot.

**One-time setup:**
- Install Python 3 and run `pip install trimesh numpy pillow`.
- Install Blender for FBX/Blend files and very detailed models.
- The first upload asks for a GitHub token. Create a fine-grained token with access to only this repo and **Contents: Read and write**.

## Limits

- Models: around **20,000 triangles** (the script simplifies bigger ones) and 65,000 vertices.
- Photos and textures: the script resizes to **2048 px**.
- Plain OBJ files: up to 21,000 triangles, texture JPG 2048 × 2048 or smaller.

## Before each show

1. Add each exhibit with the script (or upload plain files for shareable models).
2. Wait a minute or two for GitHub Pages to update.
3. In the world, open the **Exhibit A** tab on the host terminal and add one line per exhibit:

   ```
   Shiro | 3 | Grandad's pocket watch, carried it through the war
   Ellie | 7 | Won this rubber duck at a fair in 2009
   Nobody | 12 | Spare exhibit - belongs to no contestant
   ```

   That's owner name (as their VRChat display name), slot number, then the true story (only the host and the owner see it).
4. Press **PREVIEW NEXT EXHIBIT** on the terminal to check each one loads, then **STOP**.

## Making a model from a real object

Scan it with a phone app such as **Scaniverse** (free, iOS/Android), export as OBJ or GLB, and run it through the script.
