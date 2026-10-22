# Clippy for Codex

An unofficial animated Clippy companion for the Codex desktop app. The classic silver paperclip blinks, looks around, waves, jumps, and reacts to what Codex is doing.

<p align="center">
  <img src="assets/clippy-demo.gif" alt="Animated Clippy waving and looking around" width="84" height="123">
</p>

The pet has a transparent background. Its sprite sheet uses the Codex v2 format: **8 columns × 11 rows**, with **192 × 208 px** cells (1536 × 2288 px total). It includes nine standard animation rows and 16 look directions.

## Install

These instructions are for the **Codex desktop app's local pet picker**. This repository is not a Codex CLI plugin or a ChatGPT Work pet.

### 1. Download this repository

Clone it:

```sh
git clone https://github.com/develmax/codex-clippy-pet.git
cd codex-clippy-pet
```

Or choose **Code → Download ZIP** on GitHub, extract it, and open a terminal in the extracted `codex-clippy-pet-main` folder. The following commands assume your terminal is in the repository root, where the `clippy` folder is visible.

### 2. Copy the pet into your Codex home directory

Codex reads local custom pets from `pets/<pet-id>/` under `CODEX_HOME`. If `CODEX_HOME` is not set, use `~/.codex`. The final layout must be:

```text
<Codex home>/
└── pets/
    └── clippy/
        ├── pet.json
        └── spritesheet.webp
```

**Windows — PowerShell**

Run this from the repository root:

```powershell
$CodexHome = if ($env:CODEX_HOME) { $env:CODEX_HOME } else { Join-Path $HOME '.codex' }
$Target = Join-Path $CodexHome 'pets\clippy'
New-Item -ItemType Directory -Force -Path $Target | Out-Null
Copy-Item -LiteralPath '.\clippy\pet.json', '.\clippy\spritesheet.webp' -Destination $Target -Force
Get-ChildItem -LiteralPath $Target
```

With the default Codex home, this installs to `%USERPROFILE%\.codex\pets\clippy\`.

**macOS or Linux — Terminal**

Run this from the repository root:

```sh
CODEX_DIR="${CODEX_HOME:-$HOME/.codex}"
mkdir -p "$CODEX_DIR/pets/clippy"
cp ./clippy/pet.json ./clippy/spritesheet.webp "$CODEX_DIR/pets/clippy/"
ls -l "$CODEX_DIR/pets/clippy/"
```

### 3. Select Clippy in Codex

Restart the Codex desktop app if it was open while you copied the files. Open Codex settings, find the pet selector, and choose **Clippy**. The exact settings label may differ between app versions.

## If Clippy does not appear

1. Check that both `pet.json` and `spritesheet.webp` are directly inside `pets/clippy/`. An extra nested `clippy/clippy/` folder will prevent discovery.
2. Check whether `CODEX_HOME` is set. If it is, install under that directory rather than `~/.codex`.
3. Close and reopen the Codex desktop app after copying the files.
4. Open `pet.json` and confirm that `id` is `clippy`, `spriteVersionNumber` is `2`, and `spritesheetPath` is `spritesheet.webp`.
5. Use a Codex desktop version with the custom pet picker. The CLI alone does not display an animated desktop pet.

To update Clippy later, replace both files in the same `pets/clippy/` folder and restart Codex. To remove it, delete that folder.

## What's in the repository

```text
clippy/
  pet.json                 Pet metadata and v2 sprite version
  spritesheet.webp         Transparent 8 × 11 animation atlas
assets/
  clippy-demo.gif          Small animated preview; not needed for installation
  spritesheet-preview.png  Overview of all animation frames; not needed for installation
```

The standard rows cover idle, movement to the right and left, waving, jumping, failure, waiting for your attention, active work, and review/ready state. The last two rows provide 16 clockwise look directions. [Inspect the complete frame sheet](assets/spritesheet-preview.png).

## About this project

This is a fan-made project and is not affiliated with or endorsed by Microsoft or OpenAI. Clippy is a Microsoft character; Codex is an OpenAI product. The included art was made for this custom pet.
