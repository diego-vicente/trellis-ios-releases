# Trellis iOS — release channel

Public host for the **[Trellis](https://github.com/diego-vicente/trellis) iOS app** so it can be
installed and auto-updated through **[SideStore](https://sidestore.io)** without a paid Apple
Developer account. This repo holds only the release `.ipa`s (as GitHub Releases) and the SideStore
source manifest — **no app source code** (that stays in the private app repo).

## Add the source in SideStore

In SideStore → **Sources → +**, add:

```
https://raw.githubusercontent.com/diego-vicente/trellis-ios-releases/main/apps.json
```

Then install **Trellis** from the source. With auto-updates on, SideStore refreshes the signature
and pulls new versions in the background.

## How releases are made

iOS apps must be built on macOS + Xcode, so builds run **locally on the Mac**, not in CI. From the
app repo, `scripts/release.sh`:

1. builds a Release `.ipa` (`xcodebuild`, `MARKETING_VERSION = 1.0.<git-commit-count>`),
2. creates a GitHub Release here with the `.ipa`,
3. prepends the new version to `apps.json` and pushes.

SideStore then sees the new version at the source URL above.
