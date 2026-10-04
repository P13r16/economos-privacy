# Economos privacy policy

The published policy for **Economos**, the offline subscription tracker for
Android.

- **Published at:** https://p13r16.github.io/economos-privacy/
- **Source of truth:** [`index.html`](index.html) in this repository
- **App source:** https://github.com/P13r16/Economos

## What it says, in one line

Economos collects nothing, and the Android app does not request the
`android.permission.INTERNET` permission at all, so the operating system prevents
it from sending your data anywhere.

## Why this repository exists

Google Play requires a privacy policy at a stable, publicly reachable URL for
every app listing. This repo hosts that page on GitHub Pages, which is free,
HTTPS by default, and cannot be taken down by a hosting provider's terms
changing.

The page itself loads no third-party resources, for the same reason the app
does not: no web fonts, no analytics, no trackers, no network requests.

## Verifying the claims

Every factual claim on the policy page was checked against the signed release
build rather than assumed. To reproduce:

- **No internet permission.** Read the merged release manifest at
  `android/app/build/intermediates/merged_manifest/release/processReleaseMainManifest/AndroidManifest.xml`
  and confirm the only `uses-permission` entries are `POST_NOTIFICATIONS`,
  `RECEIVE_BOOT_COMPLETED`, `WAKE_LOCK` and the AndroidX-generated
  `DYNAMIC_RECEIVER_NOT_EXPORTED_PERMISSION`.
- **Backup is off.** Confirm `android:allowBackup="false"` in the same manifest,
  alongside `android:dataExtractionRules` and `android:fullBackupContent`.
- **No third-party SDKs.** Confirm the Capacitor plugin list is filesystem,
  local-notifications and share only.

`src/android-config.test.ts` asserts the manifest and backup rules in CI, so a
regression that reintroduced a network permission would fail the test suite
rather than quietly invalidating this page.

## Before publishing

Replace `CONTACT_EMAIL_PLACEHOLDER` in `index.html` with a real monitored email
address, then commit. Google Play requires a contact address, and a placeholder
is worse than none because it looks live.

## Reviewing changes

If any future release changes what the app does, update this page in the same
change. In particular, the day a paid option is added, the "In-app purchases"
section and the Play Data safety form must both be updated before release.