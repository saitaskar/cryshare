# CryShare

CryShare is a personal fork of [ShareX](https://github.com/ShareX/ShareX), the open-source
screen capture, file sharing and productivity tool. All credit for the application goes to
the ShareX Team. This fork exists so I can tweak defaults and behavior for my own daily use.

It is licensed under the **GNU General Public License v3**, same as ShareX. See `LICENSE.txt`.

## Download / Install

Grab the latest installer from the releases page:

**https://github.com/saitaskar/cryshare/releases/latest**

Under **Assets**, download and run `CryShare-<version>-setup-x64.exe`. It installs to its own
`Program Files\CryShare` and stores settings in `Documents\CryShare`, so it never touches an
existing ShareX install. Prefer no installer? Use the `-portable-x64.zip` instead.

The installer is unsigned, so Windows SmartScreen shows a warning the first time. Click
**More info -> Run anyway**.

## What's different from ShareX

- Rebranded to CryShare (window title, tray, installer, Start Menu).
- Runs side-by-side with a stock ShareX install: its own single-instance mutex and its own
  settings folder (`Documents\CryShare`), so it never touches an existing ShareX setup.
- Auto-updates from this repository's GitHub Releases instead of the official ShareX repo.
- Everything else is stock ShareX.

## Auto-update

CryShare checks `github.com/saitaskar/cryshare` releases on startup (same mechanism ShareX
uses for itself, just repointed). Pushing a `vX.Y.Z` tag triggers CI, which builds the
`Release x64` setup and portable zip and publishes them as a GitHub Release. The running app
sees the new `vX.Y.Z` tag, downloads `CryShare-X.Y.Z-setup-x64.exe`, and updates itself.

### Cutting a release

1. Bump `<Version>` in `Directory.build.props` (optional, CI overrides it from the tag).
2. `git tag vX.Y.Z && git push origin vX.Y.Z`
3. CI builds and publishes the release. The installed app picks it up on next update check.

## Building locally

Requires the .NET 10 SDK and (for the installer) Inno Setup 6.

```powershell
dotnet build ShareX.sln -c Release -p:Platform=x64
# app: ShareX\bin\Release\win-x64\ShareX.exe
```

## Upstream

To pull in new ShareX changes, add the upstream remote and merge:

```powershell
git remote add upstream https://github.com/ShareX/ShareX.git
git fetch upstream
git merge upstream/develop
```

The rebrand is kept intentionally small (a handful of files) so these merges stay easy.
