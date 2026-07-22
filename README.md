# Philosophy
- Packages that hold configs have the suffix of '-config' e.g. `bitglyph-kde-config`.
- If there is a meta package, e.g. "bitglyph-plasma-meta", that meta can just have bitglyph-kde-config as a dependency

Meta packages should stay PURE meta packages, separate from the configs, literally just "depends".

If a meta package MUST contain a config, then it should be its own separate pkgbuild, with -config at the end.

All meta packages should strictly be in the manifest.yaml

# What happens when a meta package updates