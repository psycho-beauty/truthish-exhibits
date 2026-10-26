# Truthish – Exhibit files

This repo feeds the **Exhibit A** hologram projector in the Truthish VRChat world.
The world loads files from `https://psycho-beauty.github.io/truthish-exhibits/` at show time,
so you can change exhibits without re-uploading the world.

## Slots

There are 24 slots. Each slot can have a 3D model, a photo, or both:

| File | What it is |
| --- | --- |
| `exhibit01.obj` … `exhibit24.obj` | 3D model, shown as a spinning hologram |
| `exhibit01.jpg` … `exhibit24.jpg` | Photo. Used as the model's texture, or shown on its own if there's no model |

- Names must be exactly like this: lowercase, two digits (`exhibit03.obj`, not `Exhibit3.OBJ`).
- If a slot has neither file, the projector shows "SIGNAL LOST".
- `exhibit24` holds a sample trophy you can use to test. Replace it whenever you like.

## Limits

- **Models:** OBJ only, up to about **20,000 triangles**. Anything over 21,000 is cut off. Smaller loads faster.
- **Photos:** JPG, **2048 × 2048 pixels or smaller**. Larger images fail to load.
- No `.mtl` file is needed. Colour comes from the matching `.jpg`, if there is one.
- Everything here is **public**. Only upload what contestants are happy to share.

## Before each show

1. Collect each contestant's photos or scans and the true story behind each one.
2. Name the files by slot and upload them here (drag and drop on github.com works).
3. Wait a few minutes for GitHub Pages to update. You can watch the Actions tab.
4. In the world, open the **Exhibit A** tab on the host terminal and add one line per exhibit:

   ```
   Shiro | 3 | Grandad's pocket watch, carried it through the war
   Ellie | 7 | Won this rubber duck at a fair in 2009
   Nobody | 12 | Spare exhibit - belongs to no contestant
   ```

   That's owner name (as their VRChat display name), slot number, then the true story (only the host and the owner see it).
5. Press **PREVIEW NEXT EXHIBIT** on the terminal to check each one loads, then **STOP**.

## Making a model

**Scan a real object with a phone.** For example, use **Scaniverse** (free, iOS/Android):

- Scan the object, then Share/Export → **OBJ**, at the lowest detail option.
- You'll get a model file and a texture image. Rename them to `exhibitNN.obj` and `exhibitNN.jpg`.

**Clean it up in Blender** (if it's too detailed, or it's an FBX/GLB):

1. File → Import the model.
2. Select it. Add Modifier → **Decimate**, then lower the Ratio until the triangle count (shown in the status bar) is under 20,000. Apply it.
3. File → Export → **Wavefront (.obj)**. Tick *Selection Only* and *UV Coordinates*. You can untick *Materials* and *Normals*.
4. Export the texture as JPG, 2048 px or smaller.

Models are automatically centred, scaled to about 2.2 m and stood upright on the projector, so size doesn't matter. "Up" should be +Y, which is the Blender OBJ export default.
