# Mandoobi releases

Update feed and APK downloads for the Mandoobi app (it isn't on any store).

- `appcast.xml` is read by the app on launch. When it lists a version newer
  than the installed one, the app shows an update popup.
- Each version's APK is attached to the matching GitHub release (`v1.2.3`).

## Publishing a version

From the app project:

1. Bump `version:` in `pubspec.yaml`. Raise both the name and the build number
   (e.g. `1.0.0+1` -> `1.0.1+2`). The app compares the name; Android needs a
   higher build number to install over the old APK.
2. Run `tool/release.sh "release notes"` (add `--critical` to force the update:
   the popup then has no Later / Ignore buttons).

The script builds the signed APK, creates the GitHub release and adds the
version to `appcast.xml`.

## Manual item format

```xml
<item>
  <title>Version 1.0.1</title>
  <description>Release notes shown in the popup</description>
  <pubDate>Wed, 30 Sep 2026 12:00:00 +0000</pubDate>
  <enclosure url="https://github.com/amr-alawaad99/mandoobi-releases/releases/download/v1.0.1/mandoobi-1.0.1.apk"
             sparkle:version="1.0.1" sparkle:os="android"
             type="application/vnd.android.package-archive" />
  <!-- optional, forces the update: -->
  <sparkle:tags><sparkle:criticalUpdate /></sparkle:tags>
</item>
```
