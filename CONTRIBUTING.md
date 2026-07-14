# Contributing Packages

Package publication is a pull request against this repository. There is no
registry server and no `encore publish` command in Encore v1.

## New Package

1. Publish a signed or annotated version tag in the package source repository.
2. Build a reproducible `.tar.gz` with `encore.toml` at its root and without
   generated build output.
3. Run `encore test` against the packaged source.
4. Upload the exact archive as a GitHub Release asset.
5. Compute its lowercase SHA-256.
6. Add `<first-two-characters>/<name>.json` in a fork of this repository.
7. Open a pull request containing only the package metadata change.

Package names must match `^[a-z0-9_-]{2,}$`. Published manifests may use
`index@` or explicit `git@` dependencies but may not use local `path@`
dependencies.

```json
{
  "name": "example_math",
  "versions": [
    {
      "version": "1.0.0",
      "archive": "https://github.com/author/example_math/releases/download/v1.0.0/example_math-1.0.0.tar.gz",
      "checksum": "0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef",
      "yanked": false
    }
  ]
}
```

## New Version

Append the new version object to the existing `versions` array. Do not modify
or reorder old objects. Every version needs a unique SemVer and immutable asset
URL.

The v1 resolver selects the last non-yanked entry, so entries must stay in
release order.

## Yank

Change only the affected version's `yanked` field from `false` to `true`. Do
not delete its metadata or archive. Yanking prevents new resolution while
preserving existing lockfiles.

## Automated Checks

Index CI verifies:

- metadata location and JSON schema;
- package names and SemVer versions;
- unique versions and immutable existing records;
- HTTPS GitHub archive URLs and lowercase SHA-256 values;
- downloaded archive checksum and safe member paths;
- root `encore.toml` name/version identity;
- absence of `path@` dependencies in published manifests.

Maintainers additionally review source ownership, licensing, dependency
choices, package quality, and test evidence. Passing CI does not guarantee
acceptance.
