# eaw-baseline

The shipped-game index the Empire at War language server reads: every object, asset and bone set of
the base game and the expansion, built by the server's baseline builder from the game's own files.

- `eaw/` - Empire at War
- `foc/` - Forces of Corruption, the file servers read

Each folder holds the index (`.aet`), its icon pack (`.aet.icons`) and a manifest with the index's
hash, its content version and the DTO version a server has to read to load it.

## Releases

Servers read the newest GitHub release whose tag MAJOR is the DTO version they read, never a
branch. A tag is a promise that never moves.

- Tag: `v<MAJOR>.<MINOR>.<PATCH>` - MAJOR is the DTO version (the manifest's `schemaVersion`),
  MINOR the FoC manifest's `version`, PATCH counts rebuilds at those two numbers.
- `release.json` carries the version the next release will tag.
- **Prepare Release** (Actions tab, on the branch that carries the baselines) opens the bump pull
  request; merge it. **Release** on that branch validates every baseline against its manifest, checks
  the tag against the manifests and publishes the release with the six files attached.

Servers released before 0.5.0 read `main` directly, so `main` keeps the content they can load until
those servers are out of support. Baselines for servers that read releases land on `next` and are
released from there.
