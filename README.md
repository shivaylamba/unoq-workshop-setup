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
Arduino UNO Q core
Arduino_Modulino library
Arduino_RouterBridge library
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
