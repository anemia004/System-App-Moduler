# System Moduler

A **web tool** that turns any APK into a **flashable Magisk module** – so you can install an app as a system app, systemlessly.

Just pick an APK, fill in a few details (or leave them empty to use smart defaults), and download a ready‑to‑flash `.zip` file.

## Usage

1. Open **[System Moduler](https://anemia004.github.io/system-moduler/)** in your browser.
2. Select an APK file.
3. (Optional) Fill in module ID, name, version, and author.  
   If any field is left blank, the tool uses the placeholder value as a default.
4. Tap **Generate Zip** – the zip file downloads automatically.
5. In Magisk: **Modules → Install from storage** → choose the downloaded zip.
6. Reboot. The app will appear in your app drawer as a system app.

## How it works

- All processing happens inside your browser. Your APK is **never uploaded** anywhere.
- The tool uses **JSZip** to create a valid Magisk module zip, containing:
  - `META-INF/com/google/android/update-binary` – standard Magisk installer
  - `META-INF/com/google/android/updater-script`
  - `module.prop` – with the module metadata you provide (or the defaults)
  - `customize.sh` – fixes file permissions after flashing
  - `system/priv-app/InstalledApp/<your-apk>` – the APK itself
- The generated module installs the APK as a privileged system app (via `/system/priv-app`), which allows it to retain required permissions even on modern Android versions.

## Features

- **Pure client‑side** – no server, no uploads, no sign‑ups.
- **Smart defaults** – every field has a sensible placeholder that is used when left blank.
- **Author field** – defaults to `anemia004` if you don’t change it.
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
