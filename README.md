<p align="center"><img src=".github/icon.png" width="96" alt=""></p>

# ResonanceFit releases

ResonanceFit, by Mohamed Khalil, turns a personal IEM calibration into an EQ for your ears: find your
resonance by ear in a minute, pick any target, and use the EQ in the app you listen with.

This repository only holds the release builds. The source lives in a separate repository.

## I'm a customer

You don't need anything from this page. Your tuner sends you a personal download that already holds the
app **and your calibration file** (`.rescal`) plus a calibration sheet. Unpack it, open the app, and your
calibration loads by itself. The app on its own, without a calibration file, just asks you for one.

If you lost your download, download the app for your system from
[the latest release](../../releases/latest) and open your `.rescal` file with it.

### Opening it the first time

The apps aren't code-signed yet, so your system asks once before opening them.

- **Windows:** extract the whole zip first (right-click → Extract All), then run `ResonanceFit.exe`. If
  Windows says “Windows protected your PC”, click **More info**, then **Run anyway**.
- **macOS (Apple silicon):** open the `.dmg` and drag ResonanceFit into Applications. The first time,
  right-click (or Control-click) the app, choose **Open**, then **Open** again. If macOS still refuses, go to
  System Settings → Privacy & Security and click **Open Anyway**. Then double-click your `.rescal` file once.
- **Linux (x86-64):** make the AppImage executable (right-click → Properties → Allow executing, or
  `chmod +x`) and run it, with the `Calibrations` folder from your download next to it.

Start with the volume low. Press Space at any time to stop all sound.

## Files in each release

| File | For |
|---|---|
| `ResonanceFit-<version>-windows.zip` | Windows 10 and 11, 64-bit. One folder with the app. |
| `ResonanceFit-<version>-macos.dmg` | macOS 11 or later on Apple silicon (M1 and newer). |
| `ResonanceFit-<version>-linux.AppImage` | Linux x86-64 with glibc 2.35 or later (Ubuntu 22.04+, Fedora 36+, …). |
| `SHA256SUMS` | Checksums of the files above. |

To check a download: `sha256sum -c SHA256SUMS --ignore-missing` (Linux/macOS: `shasum -a 256 -c`), or on
Windows `Get-FileHash .\ResonanceFit-<version>-windows.zip` and compare with the line in `SHA256SUMS`.

EQ Helper's “Generate customer app…” downloads the latest release from here, checks it against
`SHA256SUMS`, and packages it with each customer's calibration, so these file names must not change.

## Making a release

Releases are built by [the “Build and publish” workflow](.github/workflows/release.yml) on GitHub's
Windows, macOS and Linux runners. It checks out the source, runs the full test suite, builds the app for
each system, launches every build with `--self-test` (headless: loads a test calibration, exports for
several EQ apps, checks audio support is bundled), and only then publishes the release with
`SHA256SUMS`.

- **By hand:** Actions → Build and publish → Run workflow, enter the version (e.g. `1.0.0`) and the source
  branch or tag.
- **From a tag:** pushing `rf-v1.0.0` in the source repository starts it automatically when that
  repository has a `RELEASES_DISPATCH_TOKEN` secret (a fine-grained token with *Contents: read and write*
  on this repository).
- If the source repository becomes private, add a `SOURCE_REPO_TOKEN` secret here (*Contents: read* on
  the source repository) so the workflow can check it out.

## Licence

Apache License 2.0. See [LICENSE](LICENSE).
