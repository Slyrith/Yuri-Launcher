# Publish a launcher update

This repository is the dedicated desktop-launcher release feed: `Slyrith/Yuri-Launcher`.

## Required release assets

- `Yuri-Launcher-Official.zip` — exact filename used by the Official self-updater.
- `Yuri-Launcher-UC.zip` — manual/offline edition.
- Optional: `Yuri-Lua-SDK-v1.1-foundation.zip` and `SHA256SUMS.txt` for this version.

Upload ZIPs as **release assets**, not as ordinary files in the repository. Each ZIP must contain the complete distribution at its root: `YuriLauncher.exe`, `YuriScriptWorker.exe`, `MoonSharp.Interpreter.dll`, SDK/docs and related package files. Do not put an extra containing folder around the ZIP's contents. Do not upload private launcher source, account data or local logs.

## Version and channel

1. Increase the launcher version for each update. Use a comparable numeric tag such as `v0.11.0`, `v0.11.1`, or `v0.12.0-beta.1`. The numeric part must match the built version; reusing a tag/version for different binaries will not reliably prompt existing users.
2. Add clear release notes and the complete assets.
3. For Stable, publish a normal release and mark it **Latest**. The launcher reads GitHub's `/releases/latest` endpoint.
4. For Beta, mark the release **pre-release**. Tag suffix wording does not choose the channel; the GitHub label does. Use a higher numeric version than the installed launcher for an update prompt.
5. Confirm the GitHub release API reports a `sha256:` digest for the Official ZIP asset. Yuri requires it and verifies the downloaded file. `SHA256SUMS.txt` is useful to users but is not a replacement for that API digest.

## What users see

Official checks on startup, every 15 minutes while running, and on manual Check. A newer matching version shows a dedicated banner and download action. It stages the verified package, preserves supported local script/configuration data, and offers a separate Restart action. Older managed folders remain in place. It does not silently restart or start a game.

The Automatic checking setting controls startup and periodic checks; manual Check still works. Tray-hidden sessions continue polling. The timer stops when Yuri exits. Offline/temporary errors do not block other launcher features, and a repository with no matching release has a normal empty state.

The UC edition does not poll any online update feed and is distributed manually. Do not advertise online automatic updating for UC.

## First release checklist

For the prepared build, use tag `v0.11.0`, title **Yuri Launcher 0.11.0 — Lua SDK 1.1 & dedicated updates**, and the ZIPs supplied in the build folder. Review its changelog; choose Stable/Latest or pre-release yourself. The README's `assets/` screenshots must be uploaded with the README so its images render.

A future-version update and restart across two actually published launcher releases still needs an end-to-end live check. Current checks cover metadata selection, archive/hash validation, staging, update state and native access to the repository endpoint.
