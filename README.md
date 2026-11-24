# lightcraft-ci

GLYSK build glue for [GLYSK-OU/lightcraft](https://github.com/GLYSK-OU/lightcraft), the fork of
[storytold/lightcraft](https://github.com/storytold/lightcraft). Nothing here goes upstream.

`macos.yml` builds a branch of the fork on a GitHub macOS runner, runs the tests of chosen packages and
packages an ad-hoc-signed `LightCraft.app`, so macOS-only features (Apple Photos) can be built without a
local Rust toolchain.

```sh
gh workflow run macos.yml -R GLYSK-OU/lightcraft-ci -f ref=feat/my-branch
gh run watch -R GLYSK-OU/lightcraft-ci
gh run download -R GLYSK-OU/lightcraft-ci <run-id>
```

The downloaded app is ad-hoc signed and not notarized: after copying it to /Applications, clear the
quarantine flag with `xattr -dr com.apple.quarantine /Applications/LightCraft.app`, then open it from the
Finder so macOS asks LightCraft (not Terminal) for Photos access.
