# Sony Bravia TV Debloating

Guide to remove bloatware and speed up a Sony Bravia Android TV via ADB. The TV stays functional, but some built-in features (live TV channels, some accessibility services) may be affected. Review the package list before running.

![My Local Image](./images/screenshot1.png "Example Image")
![My Local Image](./images/screenshot.png "Example Image")

---

## Requirements

- Sony Bravia Android TV (tested on Android 9)
- ADB installed on your computer
- TV and computer on the same network

---

## Setup

Enable Developer Options:

- Navigate to: `Settings > Device Preferences > About`
- Tap `Build Number` (on some models it is instead called `Android TV OS build`) 7 times until it shows Developer Mode Enabled

Enable ADB Debugging:

- Navigate to: `Settings > Device Preferences > Developer Options` (on some models it's `Settings > System > Developer Options` instead)
- Turn on Network Debugging (or simply `ADB debugging` if you don't see that option)

Install ADB:

```bash
# Windows: download from https://developer.android.com/studio/releases/platform-tools
# macOS
brew install android-platform-tools
# Linux
sudo apt-get install android-tools-adb
```

Connect:

```bash
adb connect <TV_IP_ADDRESS>
```

List installed packages, if you want to check what's on the TV first:

```bash
adb shell pm list packages
```

---

## Uninstall script

Removes Sony and Google bloatware packages for the current user. Apps can be reinstalled later with `adb shell cmd package install-existing <package_name>`.

### Windows (cmd)

Save as `debloat.bat` and run it, or paste it into a cmd window where `adb.exe` is.

```bat
@echo off
for %%p in (
    com.sony.dtv.videoframeserver
    com.android.dreams.basic
    com.google.android.backdrop
    screenmirroring.com
    com.sony.dtv.braviasyncsetting
    com.sony.dtv.braviasyncservice
    com.android.captiveportallogin
    com.sony.dtv.customersupport
    com.sony.dtv.demomode
    com.sony.dtv.multiscreendemo
    com.sony.dtv.demosupport
    com.android.printspooler
    com.sony.dtv.reminderservice
    com.sony.dtv.da.service
    com.google.android.backuptransport
    com.google.android.play.games
    com.sony.dtv.hbbtvlauncher
    com.sony.dtv.imanual
    com.sony.dtv.smarthelp
    com.sony.dtv.homenetwork
    com.sony.dtv.interactivetvutil
    com.android.location.fused
    com.sony.dtv.tvxlauncher.titlelist
    com.sony.dtv.smartmediaapp
    com.sony.dtv.osat.music
    com.sony.dtv.b2b.hotelmode
    com.sony.dtv.tvxlauncher.programguide
    com.sony.dtv.b2b.prosettings
    com.sony.dtv.sonyselect
    com.sony.dtv.common.base.AccessibilityText
    com.sony.dtv.tvx
    com.sony.dtv.discovery
    com.sony.dtv.youview
    com.sony.dtv.promos
    com.youview.tv.servicehost
    com.sony.dtv.browser.webappruntime
    com.android.vpndialogs
    com.sony.dtv.sonyloglevelsettingvnd
    com.sony.dtv.sonyloglevelsettingsys
    com.sony.dtv.sonybugreportsys
    com.google.android.tungsten.setupwraith
    com.android.settings.intelligence
    com.sony.dtv.servicemode
    com.google.android.sss.authbridge
    tv.samba.ssm
    com.android.providers.userdictionary
    com.google.android.feedback
    com.android.providers.contacts
    com.android.providers.calendar
    com.vewd.core.integration.dia
    com.google.android.syncadapters.contacts
    com.google.android.tts
    com.google.android.videos
    com.google.android.partnersetup
    com.google.android.syncadapters.calendar
    com.google.android.katniss
    com.google.android.tv.bugreportsender
    com.google.android.tvrecommendations
    com.google.android.webview
    com.google.android.marvin.talkback
    com.sony.dtv.sonyselect.overlay
    com.sony.dtv.system.crashlog
    com.sony.dtv.b2b.rs232csupport
    com.sony.dtv.b2b.vendorprotocol
    com.sony.dtv.seconddispsetting
    com.android.wallpaperbackup
) do adb shell pm uninstall --user 0 %%p
```

### Linux / macOS (bash)

Save as `debloat.sh`, `chmod +x debloat.sh`, then run.

```bash
#!/bin/bash
packages=(
    com.sony.dtv.videoframeserver
    com.android.dreams.basic
    com.google.android.backdrop
    screenmirroring.com
    com.sony.dtv.braviasyncsetting
    com.sony.dtv.braviasyncservice
    com.android.captiveportallogin
    com.sony.dtv.customersupport
    com.sony.dtv.demomode
    com.sony.dtv.multiscreendemo
    com.sony.dtv.demosupport
    com.android.printspooler
    com.sony.dtv.reminderservice
    com.sony.dtv.da.service
    com.google.android.backuptransport
    com.google.android.play.games
    com.sony.dtv.hbbtvlauncher
    com.sony.dtv.imanual
    com.sony.dtv.smarthelp
    com.sony.dtv.homenetwork
    com.sony.dtv.interactivetvutil
    com.android.location.fused
    com.sony.dtv.tvxlauncher.titlelist
    com.sony.dtv.smartmediaapp
    com.sony.dtv.osat.music
    com.sony.dtv.b2b.hotelmode
    com.sony.dtv.tvxlauncher.programguide
    com.sony.dtv.b2b.prosettings
    com.sony.dtv.sonyselect
    com.sony.dtv.common.base.AccessibilityText
    com.sony.dtv.tvx
    com.sony.dtv.discovery
    com.sony.dtv.youview
    com.sony.dtv.promos
    com.youview.tv.servicehost
    com.sony.dtv.browser.webappruntime
    com.android.vpndialogs
    com.sony.dtv.sonyloglevelsettingvnd
    com.sony.dtv.sonyloglevelsettingsys
    com.sony.dtv.sonybugreportsys
    com.google.android.tungsten.setupwraith
    com.android.settings.intelligence
    com.sony.dtv.servicemode
    com.google.android.sss.authbridge
    tv.samba.ssm
    com.android.providers.userdictionary
    com.google.android.feedback
    com.android.providers.contacts
    com.android.providers.calendar
    com.vewd.core.integration.dia
    com.google.android.syncadapters.contacts
    com.google.android.tts
    com.google.android.videos
    com.google.android.partnersetup
    com.google.android.syncadapters.calendar
    com.google.android.katniss
    com.google.android.tv.bugreportsender
    com.google.android.tvrecommendations
    com.google.android.webview
    com.google.android.marvin.talkback
    com.sony.dtv.sonyselect.overlay
    com.sony.dtv.system.crashlog
    com.sony.dtv.b2b.rs232csupport
    com.sony.dtv.b2b.vendorprotocol
    com.sony.dtv.seconddispsetting
    com.android.wallpaperbackup
)

for p in "${packages[@]}"; do
    adb shell pm uninstall --user 0 "$p"
done
```

---

## Disable instead of uninstall

For apps you may want to keep but hidden, so they cannot be re-enabled from the TV itself:

```bash
adb shell pm disable-user --user 0 com.google.android.apps.mediashell
adb shell pm disable-user --user 0 com.android.vending
adb shell pm disable-user --user 0 com.google.android.gms
```

---

## Launcher cleanup

```bash
adb shell settings put secure tv_home_shop_content_enabled 0
adb shell settings put secure tv_home_personalized_ads_enabled 0
adb shell settings put secure tv_home_content_suggestions_enabled 0
adb shell settings put secure tv_home_promotion_tile_enabled 0
adb shell pm clear com.google.android.tvlauncher
```

---

## Performance tweaks

```bash
adb shell setprop persist.sys.input_lag 0
adb shell settings put global game_mode 1
adb shell settings put global window_animation_scale 0.5
adb shell settings put global transition_animation_scale 0.5
adb shell settings put global animator_duration_scale 0.5
adb shell pm trim-caches 999999G
```

---

## Reverting

Reinstall a removed app:

```bash
adb shell cmd package install-existing <package_name>
```

Re-enable a disabled app:

```bash
adb shell pm enable <package_name>
```

If enabling Google Play Services brings back launcher tabs:

```bash
adb shell pm clear com.google.android.tvlauncher
```
