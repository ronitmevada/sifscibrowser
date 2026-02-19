# Sifsci branding quick guide (Chromium)

This repo currently builds with Chromium defaults. If you want a Sifsci-branded build, use this sequence.

## 1) Set product identity

Primary branding values are in:

- `chrome/app/theme/chromium/BRANDING`

Typical values to keep aligned:

- `COMPANY_*`
- `PRODUCT_*`
- `COPYRIGHT`
- `MAC_BUNDLE_ID`

## 2) Replace logos and icons

For a complete visual rebrand, replace these asset families with Sifsci icons:

- App/product logos in `chrome/app/theme/chromium/`
- Platform app icons in `chrome/app/theme/` (Windows `.ico`, macOS `.icns` pipeline, Linux PNG sizes)
- Installer artwork where applicable (`chrome/installer/**`)

Tip: keep filenames the same, only replace image content. Chromium build rules already reference those paths.

## 3) Update visible product strings

Search for Chromium-visible strings and update where required:

```bash
rg "Chromium" chrome components ui ios android_webview
```

Focus on user-facing strings/resources, not comments/tests first.

## 4) Build and verify

Generate build files and build Chrome target:

```bash
gn gen out/Sifsci
ninja -C out/Sifsci chrome
```

Run:

```bash
out/Sifsci/chrome
```

Check:

- Window/app name shows **Sifsci**
- About/version dialog shows Sifsci branding
- App icon and installer name are Sifsci assets

## 5) Optional hardening for your fork

- Use a unique app id / bundle id per platform.
- Add your own update URL and policies.
- Add legal pages (Terms/Privacy) in app menu/help surfaces.

---

If you want, next step can be an automated checklist/script that validates required branding files before release.

## 6) Build on GitHub Actions and download

If your local machine is too limited, run the cloud workflow:

1. Open **Actions** tab in GitHub.
2. Run **Build Sifsci Browser (Linux)** workflow (`workflow_dispatch`).
3. After it finishes, download artifact **sifsci-linux**.
4. Extract and run `chrome` from the extracted `Sifsci/` folder.

Workflow file: `.github/workflows/build-sifsci-linux.yml`.

## 7) GitHub UI copy-paste order (no terminal)

If you are editing directly in GitHub web UI, update files in this order:

1. `.github/workflows/build-sifsci-linux.yml`
2. `README.md`
3. `chrome/app/theme/chromium/BRANDING`
4. `chrome/test/chromedriver/constants/BRANDING`
5. `docs/sifsci_branding.md`
