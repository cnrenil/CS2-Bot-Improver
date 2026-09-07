# Build

`Build.ps1` creates the same `game/csgo`-ready archive layout used by the releases. It has two intentionally separate modes:

```powershell
# Plugin-only package (used by ordinary CI)
pwsh ./build/Build.ps1 -Platform All -DownloadDependencies

# Release package with Metamod and CounterStrikeSharp
pwsh ./build/Build.ps1 -Platform All -DownloadDependencies -IncludeRuntime
```

The builder never downloads or expands a complete CS2-Bot-Improver package. It assembles the output manually from repository sources, `build/templates/`, compiled plugins, and independent component archives only. `-IncludeRuntime` resolves the latest GitHub Release assets from [Metamod:Source](https://github.com/alliedmodders/metamod-source/releases/) and [CounterStrikeSharp](https://github.com/roflmuffin/CounterStrikeSharp/releases/) and embeds only their required directories in release packages. It also extracts only the required directories from the independent Ray-Trace, Bot-Controller, Bot-Hider, and Bot-Vision releases. Panel is intentionally not built or embedded because this repository does not contain a `src-tauri` desktop wrapper. Compile-time references always come from the latest releases of [Ray-Trace](https://github.com/FUNPLAY-pro-CS2/Ray-Trace) and [CS2-Bot-Controller](https://github.com/XBribo/CS2-Bot-Controller). Use `-SkipCompile` when only repackaging.
