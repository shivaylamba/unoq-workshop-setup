# Arduino UNO Q Edge AI Workshop Setup

This repository contains the setup instructions and Windows prerequisite
installer for the workshop:

```text
Edge AI Workshop — Snapdragon AI PC + Arduino UNO Q
Gesture Detection End-to-End
```

This is **not** the face-recognition demo repository. It does not install
MobileFaceNet, CavaFace, face databases, or face-guard firmware.

The workshop setup prepares brand-new Snapdragon Windows laptops for:

```text
Arduino App Lab
Arduino UNO Q onboarding
VS Code + Remote SSH
Python development
Arduino CLI / IDE
Edge Impulse workflows
Modulino Movement / IMU gesture projects
```

## What The Installer Automates

Run this on each brand-new workshop laptop:

```powershell
winget install --source winget --id Git.Git --exact --accept-package-agreements --accept-source-agreements

cd C:\Users\Public\Downloads

git clone https://github.com/shivaylamba/unoq-workshop-setup.git

cd C:\Users\Public\Downloads\unoq-workshop-setup

Set-ExecutionPolicy -Scope Process Bypass -Force

.\scripts\Install-WorkshopPrereqs.ps1
```

The script installs or configures:

```text
Git
Python 3.11 ARM64
Google Chrome
Visual Studio Code
Arduino IDE
Arduino CLI
Arduino App Lab
Node.js LTS
Edge Impulse CLI
VS Code Remote SSH extension
VS Code Python extension
VS Code C++ extension
Optional Arduino UNO Q core/libraries when requested
Optional Edge Impulse CLI when requested
```

If `winget` cannot install a package, the script now tries direct official
download fallbacks for the major tools:

```text
Git for Windows
Python ARM64
Google Chrome
Visual Studio Code ARM64
Arduino IDE
Arduino CLI
Node.js ARM64
```

It creates:

```text
C:\ArduinoEdgeAIWorkshop
C:\ArduinoEdgeAIWorkshop\Verify-WorkshopLaptop.bat
C:\ArduinoEdgeAIWorkshop\WORKSHOP_SETUP_REPORT.txt
Desktop\Verify Edge AI Workshop Laptop.lnk
```

By default, the installer skips the slowest optional network steps:

```text
Arduino CLI core/library downloads
Edge Impulse CLI npm install
```

This is intentional for classroom setup. Arduino App Lab and Edge Impulse Studio
in the browser are enough for the workshop flow. If you explicitly need those
optional CLI tools on a prep machine, run:

```powershell
.\scripts\Install-WorkshopPrereqs.ps1 -InstallArduinoPackages -InstallEdgeImpulseCli
```

## What Still Requires Manual Work

These steps involve physical board state, App Lab UI, Wi-Fi, SSH, or account
login, so they should be completed manually during pre-workshop preparation:

```text
Connect each UNO Q with a USB-C data cable
Open Arduino App Lab
Complete first-time UNO Q onboarding
Apply board image/update prompts if App Lab shows them
Connect UNO Q to the workshop Wi-Fi
Allow Windows firewall prompts
Verify SSH access into the UNO Q
Connect the Modulino Movement sensor
Run the instructor-provided raw IMU sensor check
Confirm accelerometer/gyroscope values change when moved
Log into Edge Impulse Studio
Create or join the correct Edge Impulse project
```

## Recommended Prep Flow

For 15 laptop + UNO Q pairs:

```text
1. Run the installer on all 15 laptops.
2. Connect one UNO Q to each laptop.
3. Open Arduino App Lab and complete first-time board setup.
4. Connect each UNO Q to the workshop Wi-Fi.
5. Verify SSH access.
6. Connect Modulino Movement.
7. Run IMU sensor check.
8. Label each verified laptop + UNO Q pair as one kit.
```

Read the full plan:

```text
WORKSHOP_SETUP_ACTION_PLAN.md
```

## Winget Store Source Error

If `winget` shows this on a fresh laptop:

```text
Failed when searching source: msstore
```

force the normal `winget` source:

```powershell
winget install --source winget --id Git.Git --exact --accept-package-agreements --accept-source-agreements
```

If it still fails, reset the source cache:

```powershell
winget source reset --force
winget source update
```

If `winget` still fails for many packages, rerun the latest installer anyway.
It will attempt direct downloads from the official vendor URLs.

If the script appears stuck for a long time on a direct Chrome download but
Chrome is already installed, press `Ctrl+C`, pull the latest repo, and rerun the
installer. The current script checks for already-installed tools before trying
fallback downloads:

```powershell
cd C:\Users\Public\Downloads\unoq-workshop-setup
git pull
.\scripts\Install-WorkshopPrereqs.ps1
```

If the script is stuck on `arduino-cli core install arduino:zephyr`,
`Arduino_Modulino`, or `edge-impulse-cli`, press `Ctrl+C`, pull the latest repo,
and rerun the default installer. The current default skips those optional
network-heavy steps.
