<p align="center">
  <img src="https://user-images.githubusercontent.com/6903107/207168016-85d0dd16-1f3b-4d42-9d37-0e0d5a596ead.png" width="400">
</p>

<h1 align="center">Flow Launcher — Vim Edition <sub>(fork)</sub></h1>

<p align="center">
A community fork of <a href="https://github.com/Flow-Launcher/Flow.Launcher">Flow Launcher</a> that adds an <b>opt-in, terminal-style Vim mode</b> to the search bar.
</p>

<p align="center">
  <a href="https://github.com/namefailed/flowlauncher-vim-fork/releases/latest"><img src="https://img.shields.io/github/v/release/namefailed/flowlauncher-vim-fork?label=download&color=7389D8"></a>
  <a href="https://github.com/Flow-Launcher/Flow.Launcher/pull/4541"><img src="https://img.shields.io/badge/upstream%20PR-%234541-success"></a>
</p>

> [!NOTE]
> This is **not** the official Flow Launcher. It is a personal fork that adds Vim mode while the feature is reviewed upstream.
> The Vim feature is proposed to the official project in **[Flow-Launcher/Flow.Launcher#4541](https://github.com/Flow-Launcher/Flow.Launcher/pull/4541)** — once that merges, you can move back to official Flow Launcher and turn the same setting on there.

---

## Why this fork exists

This fork was originally built to streamline a journaling workflow: dropping long entries into a personal system through Flow Launcher, where editing a long line with plain text-box navigation is slow. Vim mode lets you drop into Normal mode, hop across word boundaries, and fix a typo without your hands leaving the home row.

The feature is **off by default** and fully self-contained — with Vim mode disabled, this build behaves exactly like upstream Flow Launcher.

## Download & install

1. Go to the **[latest release](https://github.com/namefailed/flowlauncher-vim-fork/releases/latest)**.
2. Download **`Flow-Launcher-Setup.exe`** (installer) or **`Flow-Launcher-Portable.zip`** (portable).
3. Run the installer. Windows SmartScreen may warn that the build is unsigned — this fork's releases are built by GitHub Actions from this repository's source; choose **More info → Run anyway** if you trust it.
4. Open Flow Launcher settings and enable **General → "Enable Advanced Vim Mode"**.

> Builds are produced by the [Fork Release workflow](.github/workflows/fork-release.yml) directly from this repo. If a release isn't available yet, see [Building from source](#building-from-source).

## Vim mode at a glance

- **Modes:** Insert (default) · Normal · Visual · Visual Line, with a small color-coded mode dot in the search bar.
- **Motions:** `h l w W b B e E 0 ^ $ %`, `f`/`F`/`t`/`T{char}` with `;`/`,` repeat, `j`/`k` to move through results.
- **Editing:** `x X s S r ~ dd cc D C Y p`, `gu`/`gU`, undo `u` / redo `Ctrl+R`, `.` to repeat, counts (`3w`, `d2w`).
- **Operators + text objects:** `diw`, `ci"`, `ya(`, … and the same in Visual mode.

📖 **Full keybinding reference:** [`Flow.Launcher/VimMode/README.md`](Flow.Launcher/VimMode/README.md)

## Building from source

```powershell
git clone https://github.com/namefailed/flowlauncher-vim-fork.git
cd flowlauncher-vim-fork
nuget restore
dotnet build -c Release
# Optional: produce the installer + portable zip in Output\Packages
dotnet tool install -g vpk
.\Scripts\post_build.ps1
```

Run the unit tests with `dotnet test`.

## Branches & relationship to upstream

| Branch | Purpose |
| --- | --- |
| **`dev`** (this branch) | The fork's default branch: fork branding + the [release workflow](.github/workflows/fork-release.yml). What you download from Releases. |
| **`vim-mode`** | The clean branch behind upstream **[PR #4541](https://github.com/Flow-Launcher/Flow.Launcher/pull/4541)** — kept identical to upstream `dev` plus the feature, with no fork-specific changes. |

These two branches stay in sync automatically: a scheduled job ([`sync-dev.yml`](.github/workflows/sync-dev.yml), every 30 min, or run on demand) merges `vim-mode` into `dev` (the fork-only files above are preserved), and any update to `dev` builds and publishes a fresh [release](https://github.com/namefailed/flowlauncher-vim-fork/releases/latest) via [`fork-release.yml`](.github/workflows/fork-release.yml). So work happens on `vim-mode`, and a new downloadable build follows on its own.

All credit for Flow Launcher itself goes to the [Flow Launcher team and contributors](https://github.com/Flow-Launcher/Flow.Launcher/graphs/contributors). This fork only adds the Vim mode layer. For everything else — plugins, features, docs — see the official project:

[Website](https://flowlauncher.com) · [Documentation](https://flowlauncher.com/docs/) · [Official repo](https://github.com/Flow-Launcher/Flow.Launcher)
