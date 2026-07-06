# System Moduler

A **web tool** that turns any APK into a **flashable Magisk module** – install the app as a system app, systemlessly, with zero permanent changes to `/system`.

Just pick an APK, fill in a few details (only the ones marked with `*` are mandatory), and download a ready‑to‑flash `.zip` file.

## Usage

1. Open **[System Moduler](https://anemia004.github.io/system-moduler/)** in your browser.
2. Select an APK file **(\* required)**.
3. Enter a **Module ID** **(\* required)** – unique, no spaces. This determines the internal folder and prevents conflicts between modules.
4. (Optional) Fill in Module Name, Version, Version Code, and Author.  
   If any of these are left blank, the tool uses the following defaults:
   - **Module Name** → `My Module`
   - **Version** → `v1.0`
   - **Version Code** → `1`
   - **Author** → `anemia004`
5. Tap **Generate Zip** – the zip file downloads automatically.
6. In Magisk: **Modules → Install from storage** → choose the downloaded zip.
7. Reboot. The app will appear in your app drawer as a system app.

## How it works

- All processing happens inside your browser. Your APK is **never uploaded** anywhere.
- The tool uses **JSZip** to create a valid Magisk module zip, containing:
  - `META-INF/com/google/android/update-binary` – standard Magisk installer
  - `META-INF/com/google/android/updater-script`
  - `module.prop` – with the metadata you provide (or the defaults)
  - `customize.sh` – fixes file permissions after flashing
  - `system/priv-app/<ModuleID>/<YourAPK>` – the APK itself
- The generated module installs the APK as a privileged system app (via `/system/priv-app`), which allows it to retain required permissions even on modern Android versions.
- The folder inside `priv-app` is named after your **Module ID**, so every module gets its own unique directory and never overwrites another.

## Features

- **Pure client‑side** – no server, no uploads, no sign‑ups.
- **Smart defaults** – only two fields are required; the rest use sensible placeholders.
- **Unique folder names** – derived from your Module ID to avoid conflicts when multiple modules are flashed.
- **Instant download** – the zip is generated directly in the browser and saved immediately.
- **Systemless** – your actual `/system` partition is never modified; Magisk handles everything in memory.

## Requirements

- A device with **Magisk v20.4+** installed.
- The APK you want to convert.

## Add to Home Screen (mobile)

For a quick, app‑like experience, open the page in your mobile browser and choose **“Add to Home screen”**. It will launch in full‑screen mode without any browser interface.

## Credits

Built by [anemia004](https://github.com/anemia004)  
Uses [JSZip](https://stuk.github.io/jszip/) library
