<p align="center">
  <img src="https://i.postimg.cc/hvMGMFFS/banner.png" alt="HostsGuard Hosts File Manager — Visual Windows Hosts Editor & Profile Switcher" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Hosts%20Profile%20Manager-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-hostsguard--v1.2-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# HostsGuard Hosts File Manager — Visual Windows Hosts Editor & Profile Switcher

**Tired of opening Notepad as Administrator, hunting down C:\Windows\System32\drivers\etc\hosts, and manually running ipconfig /flushdns every time you test local dev domains or block telemetry? Manage toggleable hosts profiles visually with automatic backups.**

HostsGuard Hosts File Manager turns Windows `hosts` editing into a safe, reversible workflow: **organizing domain rules into named profiles (`Default`, `Local Dev`, `Privacy Block`), letting you toggle individual IP-to-hostname rows with checkboxes, and flushing the Windows DNS cache automatically on save**.

This project is aimed at **Windows 10 and Windows 11 (64-bit) developers, sysadmins, and privacy-focused users** managing local domain mappings cleanly.

## Quick Use-Case & Troubleshooting Reference

| Scenario / Issue | Cause | Solution |
| --- | --- | --- |
| Editing `System32\drivers\etc\hosts` fails with 'Access Denied' | Windows protects the `etc\hosts` file from non-elevated editors | Edit safely with automatic UAC elevation and timestamped backups |
| Browser still loads old IP after editing `hosts` | Windows DNS resolver cache holds stale entries after file edits | Automatically run `ipconfig /flushdns` whenever changes are applied |
| Switching between Work VPN, Local Dev, and Default setups | Commenting out 30 lines with `#` manually is tedious | Toggle entire named profiles on/off with one checkbox |
| Accidental syntax typo corrupts `hosts` formatting | Missing spaces or invalid IPv4/IPv6 syntax breaks resolution | Validate IP addresses and hostnames before writing to disk |

## Download for Windows

[**Download HostsGuard.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/HostsGuard.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why use `HostsGuard.exe`? (Key features)

- Visual table editor with individual enable/disable checkboxes (`#` comment toggling) for every host entry.
- Supports multiple named profiles (`Default`, `Local Dev`, `Telemetry Block`) that can be toggled independently.
- Creates an automatic timestamped backup of `etc\hosts` before every save.
- Flushes the Windows DNS resolver cache automatically upon saving so changes take effect immediately.

### Sample Output

```text
[HostsGuard] Loaded: C:\Windows\System32\drivers\etc\hosts (38 active entries)
[OK]   Backup Saved     : %APPDATA%\HostsGuard\backups\hosts_2026-11-23.bak
[OK]   Profile Toggled  : [ON] Local_Dev (127.0.0.1 app.local, api.local)
[OK]   DNS Cache        : Windows DNS Resolver Cache flushed successfully
```

The release ZIP is named `HostsGuard.zip`; the Windows executable inside is named `HostsGuard.exe`.

1. Close HostsGuard before updating or replacing executable files.
2. Click **Download HostsGuard.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `HostsGuard.exe`.
5. Review the options and output paths before processing files.

**Requirements:** Windows 10 or 11 (64-bit); requires Administrator rights when writing to `System32\drivers\etc\hosts`.

### Verification & Windows SmartScreen Note

- **Offline & standard user permissions:** `HostsGuard.exe` runs locally without uploading your files and does not require disabling Windows Defender.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project solves

### No more hunting hidden `System32\drivers\etc` paths

Opens directly to your active `hosts` entries and custom profiles.

### Automatic DNS flush on every save

Eliminates confusion when browsers ignore newly added `127.0.0.1` entries.

### Timestamped rollback backups

Restore any previous version of your `hosts` file in one click.

### Built-in IPv4/IPv6 syntax validation

Prevents malformed lines from breaking local name resolution.

## Default folders and configuration paths

HostsGuard manages Windows' system `hosts` file and stores profile backups in `%APPDATA%\HostsGuard`:

```text
C:\Windows\System32\drivers\etc\hosts
```

Typical directory layout:

```text
C:\Windows\System32\drivers\etc\hosts
%APPDATA%\HostsGuard\
├── profiles\
│   ├── local_dev.hosts
│   └── privacy_block.hosts
└── backups\
    └── hosts_2026-11-23.bak
```

If third-party antivirus software locks `etc\hosts` against modification, allow HostsGuard in your AV settings.

## Quick start guide

Follow these steps to get started:

1. **Extract `HostsGuard.zip` and launch `HostsGuard.exe`.** Accept the UAC prompt so HostsGuard can read/write `etc\hosts`.
2. **Add new `IP -> Domain` entries or toggle existing checkboxes.** Organize recurring rules into named profiles.
3. **Click **Save & Flush DNS**.** HostsGuard backs up your current `hosts` file, writes the update, and flushes DNS.
4. **Use **Restore Backup** anytime to revert to a previous snapshot.** Verify resolution immediately in your browser or terminal.

### Data safety note

HostsGuard automatically creates a backup in `%APPDATA%\HostsGuard\backups` before writing any change.

## What the status summary shows

HostsGuard displays **active entry count, enabled profiles, backup snapshot path, and DNS flush confirmation**.

## FAQ

**Why does HostsGuard ask for Administrator permission?**

Windows restricts write access to `C:\Windows\System32\drivers\etc\hosts` to administrators for system security.

**Do I need to run ipconfig /flushdns manually after saving?**

No—HostsGuard flushes the Windows DNS cache automatically every time you click Save.

**Can I restore my original default Windows hosts file?**

Yes—click 'Restore Default Windows Hosts' in the toolbar.

## Useful reading

- [Microsoft Support — How to Reset the Hosts File Back to Default](https://support.microsoft.com/en-us/topic/how-to-reset-the-hosts-file-back-to-the-default-c2a43f9d-e176-c6f3-e4ef-3500277a6dae)

## More Windows Desktop Utilities

- [PortWatch-LocalPortKiller](../PortWatch-LocalPortKiller) — Find & free blocked Windows TCP/UDP ports in one click
- [NetPing-DNSGameSwitcher](../NetPing-DNSGameSwitcher) — Game server ping tester, Winsock reset & DNS switcher
- [Win11-GamingDebloatGuard](../Win11-GamingDebloatGuard) — Windows 11 gaming optimizer & background process cleaner
- [ClipVault-OfflineClipboardHistory](../ClipVault-OfflineClipboardHistory) — Offline Windows clipboard history & plain-text snippet manager

*Independent open-source desktop utility for Windows.*
