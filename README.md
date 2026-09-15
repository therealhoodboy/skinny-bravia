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

## App overview

Below is what each package does, grouped by category. Use this to decide what to keep before running the script. Uninstall syntax:

```bash
adb shell pm uninstall --user 0 <package_name>
```

### Sony Bloatware

| App Name                    | Package Name                      | Purpose                           |
| ---------------------------- | ---------------------------------- | ---------------------------------- |
| Sony Video Frame Server     | `com.sony.dtv.videoframeserver`   | Frame rendering service           |
| Sony Demo Mode              | `com.sony.dtv.demomode`           | TV demo mode                      |
| Sony HbbTV Launcher         | `com.sony.dtv.hbbtvlauncher`      | HbbTV interface                   |
| Sony iManual                | `com.sony.dtv.imanual`            | TV user manual                    |
| Sony Smart Help             | `com.sony.dtv.smarthelp`          | Smart help service                |
| Sony Reminder Service       | `com.sony.dtv.reminderservice`    | TV reminder service               |
| Sony Discovery              | `com.sony.dtv.discovery`          | Content recommendation            |
| Sony YouView                | `com.sony.dtv.youview`            | TV content aggregation            |
| YouView Service Host        | `com.youview.tv.servicehost`      | Host for YouView service          |
| Sony Multi-Screen Demo      | `com.sony.dtv.multiscreendemo`    | Multi-screen demo                 |
| Sony Demo Support           | `com.sony.dtv.demosupport`        | Support for demo mode             |
| Sony Home Network           | `com.sony.dtv.homenetwork`        | Home network service              |
| Sony Interactive TV Utility | `com.sony.dtv.interactivetvutil`  | Interactive TV service            |
| Sony Select                 | `com.sony.dtv.sonyselect`         | Sony content store                |
| Sony Select Overlay         | `com.sony.dtv.sonyselect.overlay` | Sony content overlay              |
| Samba TV                    | `tv.samba.ssm`                    | TV content recommendation service |

### Sony System Services

| App Name                    | Package Name                         | Purpose                   |
| ---------------------------- | -------------------------------------- | --------------------------- |
| Sony BraviaSync Setting     | `com.sony.dtv.braviasyncsetting`     | Bravia Sync configuration |
| Sony BraviaSync Service     | `com.sony.dtv.braviasyncservice`     | Bravia Sync service       |
| Sony Browser WebApp Runtime | `com.sony.dtv.browser.webappruntime` | Web app execution service |
| RS232 Support               | `com.sony.dtv.b2b.rs232csupport`     | RS232 support             |
| B2B service                 | `com.sony.dtv.b2b.vendorprotocol`    | Unknown b2b service       |
| PiP service                 | `com.sony.dtv.seconddispsetting`     | PiP Service (TV)          |

### Sony Enhanced Services

| App Name          | Package Name                   | Purpose                |
| ------------------ | -------------------------------- | ------------------------ |
| Sony Pro Settings | `com.sony.dtv.b2b.prosettings` | PRO settings           |
| Sony Hotel Mode   | `com.sony.dtv.b2b.hotelmode`   | PRO mode / Hotel mode  |
| Sony Service Mode | `com.sony.dtv.servicemode`     | Developer service mode |

### Sony Diagnostics Services

| App Name                       | Package Name                          | Purpose                  |
| -------------------------------- | ---------------------------------------- | --------------------------- |
| Sony Log Level Settings Vendor | `com.sony.dtv.sonyloglevelsettingvnd` | Vendor logging settings  |
| Sony Log Level Settings System | `com.sony.dtv.sonyloglevelsettingsys` | System logging settings  |
| Sony Bug Report System         | `com.sony.dtv.sonybugreportsys`       | Bug report service       |
| Sony Crash Report System       | `com.sony.dtv.system.crashlog`        | Crash report service     |
| Sony Customer Support          | `com.sony.dtv.customersupport`        | Customer support service |
| Sony DA Service                | `com.sony.dtv.da.service`             | Remote support           |

### Sony Applications

| App Name             | Package Name                    | Purpose             |
| ---------------------- | ---------------------------------- | ---------------------- |
| Vewd Browser         | `com.vewd.core.integration.dia` | Web browser         |
| Sony Smart Media App | `com.sony.dtv.smartmediaapp`    | Media player        |
| Sony OSAT Music      | `com.sony.dtv.osat.music`       | Music player        |
| Sony Promos          | `com.sony.dtv.promos`           | Promotional content |
| Screen Mirroring     | `screenmirroring.com`           | Mirroring service   |

### Sony Television Services

| App Name                        | Package Name                            | Purpose              |
| ---------------------------------- | ------------------------------------------ | ----------------------- |
| Sony TVX Launcher Title List    | `com.sony.dtv.tvxlauncher.titlelist`    | Recorded TV programs |
| Sony TVX Launcher Program Guide | `com.sony.dtv.tvxlauncher.programguide` | TV program guide     |
| Sony TVX                        | `com.sony.dtv.tvx`                      | TV core service      |

### Accessibility Services

| App Name                | Package Name                                 | Purpose                |
| -------------------------- | ----------------------------------------------- | ------------------------- |
| Sony Accessibility Text | `com.sony.dtv.common.base.AccessibilityText` | Accessibility settings |
| Google Text-to-Speech   | `com.google.android.tts`                     | Text-to-speech engine  |
| Google Talkback         | `com.google.android.marvin.talkback`         | Accessibility service  |

### Android Diagnostic Services

| App Name                    | Package Name                            | Purpose                       |
| ------------------------------ | ------------------------------------------ | -------------------------------- |
| Google TV Bug Report Sender | `com.google.android.tv.bugreportsender` | Send TV bug reports to Google |
| Google Feedback             | `com.google.android.feedback`           | Google feedback service       |

### Android System Services

| App Name                     | Package Name                               | Purpose                       |
| ------------------------------- | --------------------------------------------- | -------------------------------- |
| Captive Portal Login         | `com.android.captiveportallogin`           | Network captive portal        |
| VPN Dialogs                  | `com.android.vpndialogs`                   | VPN configuration             |
| Android Location Fused       | `com.android.location.fused`               | Location services             |
| Google Backup Transport      | `com.google.android.backuptransport`       | Backup data to Google         |
| Print Spooler                | `com.android.printspooler`                 | Print management service      |
| Google Backdrop              | `com.google.android.backdrop`              | Picture frame service         |
| Google SSS Authbridge        | `com.google.android.sss.authbridge`        | Google authentication bridge  |
| Google Tungsten Setup Wraith | `com.google.android.tungsten.setupwraith`  | TV setup wizard               |
| Google Webview               | `com.google.android.webview`               | Web rendering engine          |
| Google Contacts Sync         | `com.google.android.syncadapters.contacts` | Sync contacts with Google     |
| Google Calendar Sync         | `com.google.android.syncadapters.calendar` | Sync calendar with Google     |
| Google Search (Katniss)      | `com.google.android.katniss`               | Google search integration     |
| Contacts Provider            | `com.android.providers.contacts`           | Manage and store contacts     |
| Calendar Provider            | `com.android.providers.calendar`           | Calendar data provider        |
| Google TV Recommendations    | `com.google.android.tvrecommendations`     | Google TV content suggestions |
| Settings Intelligence        | `com.android.settings.intelligence`        | Google smart settings         |
| Android Dreams Basic         | `com.android.dreams.basic`                 | Screen saver service          |
| User Dictionary Provider     | `com.android.providers.userdictionary`     | Personal dictionary           |
| Android Wallpaper Backup     | `com.android.wallpaperbackup`              | Wallpaper backup service      |

### Google Applications

| App Name             | Package Name                      | Purpose                      |
| ---------------------- | ------------------------------------ | ------------------------------- |
| Google Play Games    | `com.google.android.play.games`   | Google Play Games service    |
| Google Play Movies   | `com.google.android.videos`       | Google movie service         |
| Google Partner Setup | `com.google.android.partnersetup` | Google partner configuration |

---

## Uninstall script

Removes all Sony and Google bloatware packages listed above for the current user.  
Apps can be reinstalled later with `adb shell cmd package install-existing <package_name>`.

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
