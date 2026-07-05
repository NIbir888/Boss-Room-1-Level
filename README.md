# VEX Boss Room 1

Self-contained Unity package containing the **Boss Room 1** scene and every asset dependency it references so the scene loads with **no additional packages** required.

## What is included

- `Scenes/Boss Room 1.unity` (+ meta)
- `Dependencies/...` — every referenced asset grouped by source:
  - `shadow1/` — wall, pillar, pit, boss-room meshes/prefabs/materials/lighting
  - `bonecrusher/` — BoneCrusher statue rig + materials + textures
  - `srrubfishvfx03/` — fire VFX materials + textures
  - `pilotostudio1/` — Vortex swirled-dot sprite texture
  - `mk/` — MK/Toon shader files used by some boss materials
  - `com.agni.level/SampleScene/LightingData.asset` — baked lighting data
  - `Assets/...` — Rubfish VFX textures/shaders/meshes, FireLevel/1.mat, Shadow1EFix SampleSceneProfile

All original `.meta` files are preserved so the GUIDs match the scene references. Folder `.meta` files are also shipped so Unity can import immutable git-package contents without needing to write anything to `Library/PackageCache/`.

## What is NOT included (Unity-shipped, always present)

The following are intentionally NOT bundled because Unity ships them in every URP / core install:

- `Packages/com.unity.render-pipelines.universal/...`
- `Packages/com.unity.render-pipelines.core/...`
- `Packages/com.unity.shadergraph/...` editor scripts
- `Library/unity default resources`

## Install

In the consumer project's `Packages/manifest.json`:

```json
"com.vex.bossroom1": "https://github.com/NIbir888/Boss-Room-1-Level.git#1.0.2"
```

Save the manifest. Unity will re-resolve and clone the package.

## CRITICAL: first-time import step

Even with folder metas shipped, Unity 6 sometimes skips importing `.unity` scene files inside git-package subfolders during the **initial** package install. If `Packages/com.vex.bossroom1/Scenes/` shows empty **the first time** you install v1.0.2, do this **once**:

1. In the Project window, navigate to `Packages/com.vex.bossroom1`
2. Right-click the `Scenes` folder → **Reimport**
3. Wait for the import to finish (check the spinner in the bottom-right)
4. `Boss Room 1.unity` will now appear

After that one-time reimport, the scene will persist across restarts.

## Verify

```text
Window > General > Search : "Boss Room 1"
```

You should see:

```text
Packages/com.vex.bossroom1/Scenes/Boss Room 1.unity
```

## Known issues carried over from the source

```text
1. SampleScene/LightingData.asset (from the original Shadow1E V1 package)
   fails to load with an "Unknown error" — inherited limitation.
2. MK/Toon shaders declare _EnableRukhanka outside UnityPerMaterial.
   May print a BatchDrawCommand warning if GPU Resident Drawer is enabled.
```
