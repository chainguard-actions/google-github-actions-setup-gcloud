<!-- markdownlint-disable -->

# Hardening Report: google-github-actions--setup-gcloud/v3.0.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **google-github-actions--setup-gcloud/v3.0.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Three workflow files reference external actions or reusable workflows using mutable tags instead of full 40-character commit SHAs, making them vulnerable to supply-chain attacks if the tag is moved.

- draft-release.yml: `uses: 'google-github-actions/.github/.github/workflows/draft-release.yml@v3'` — mutable tag `@v3`
- integration.yml: `uses: 'google-github-actions/auth@v2'` (appears twice, marked `# ratchet:exclude`) — mutable tag `@v2`
- release.yml: `uses: 'google-github-actions/.github/.github/workflows/release.yml@v3'` — mutable tag `@v3`

All of these should be pinned to a full SHA, e.g. `uses: 'google-github-actions/auth@<40-hex-sha> # v2'`.

Locations:

- `.github/workflows/draft-release.yml:16`
- `.github/workflows/integration.yml:50`
- `.github/workflows/integration.yml:65`
- `.github/workflows/release.yml:9`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned all four mutable tag references to full commit SHAs:
1. draft-release.yml line 16: `google-github-actions/.github/.github/workflows/draft-release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`
2. integration.yml line 50: `google-github-actions/auth@v2` → `@c200f3691d83b41bf9bbd8638997a462592937ed # v2`
3. integration.yml line 65: `google-github-actions/auth@v2` → `@c200f3691d83b41bf9bbd8638997a462592937ed # v2`
4. release.yml line 9: `google-github-actions/.github/.github/workflows/release.yml@v3` → `@29c6d38eeb974133b4b66401985f7c70cf4a6681 # v3`
All SHAs were resolved via lookup_action_sha. The `# ratchet:exclude` comments were replaced with the tag name comments for readability.

