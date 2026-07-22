# Philosophy
- Packages that hold configs have the suffix of '-config' e.g. `bitglyph-kde-config`.
- If there is a meta package, e.g. "bitglyph-plasma-meta", that meta can just have bitglyph-kde-config as a dependency

Meta packages should stay PURE meta packages, separate from the configs, literally just "depends".

If a meta package MUST contain a config, then it should be its own separate pkgbuild, with -config at the end.

All meta packages should strictly be in the manifest.yaml

# Groups and release channels

Any PKGBUILD (hand-authored or generated) can declare `groups=('<name>')`.
CI (`.github/workflows/build.yml`) reads each built package's `.PKGINFO` and
routes it by group:

- No group -> the package goes to the default `stable` repo/release
  (tag `latest`).
- Any group -> the package goes *exclusively* to its own repo/release,
  tagged `<name>-latest`, with its own `bitglyph-<name>.db.tar.zst` repo db.

The group name is the only thing you declare — the release tag, repo
database, and GitHub release are all created dynamically from it, so there's
nothing else to wire up in CI to add a new channel (e.g. `personal`,
`liveonly`).

For manifest-driven meta-packages, set an optional `group: <name>` key
alongside a module (or subgroup) in `manifest.yaml` and
`ci/generate_meta_packages.py` will add the `groups=()` line for you.

# What happens when a meta package updates