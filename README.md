# Encore Package Index

This repository is the official sparse package index for the Encore language.
It stores metadata only; immutable package archives are hosted as GitHub
Release assets in package repositories or approved organization repositories.

Users normally do not clone this repository. Install a package with:

```sh
encore add <package-name>
```

Metadata is split by the first two package-name characters:

```text
json -> js/json.json
rich -> ri/rich.json
```

Each file contains all published versions in release order. Existing version
records and release assets are immutable. Broken versions are yanked rather
than deleted so existing Encore lockfiles remain reproducible.

See [CONTRIBUTING.md](CONTRIBUTING.md) to publish or yank a package. Compiler
behavior and the complete author workflow are documented in the
[Encore package guide](https://github.com/encore-language/encore/blob/trunk/docs/enbook-en/src/publishing-packages.md).
