# rising-lands-assets
# rising-lands-assets

## Verified original-data release

This repository contains the lossless extracted original Brazilian Rising Lands
resources. Code/tooling remains in the separate reverse-engineering repository;
no game engine or extractor implementation is copied here. The user authorized
publication of the resource pack.

Original download provenance, supplied by the user:
https://archive.org/download/risinglandsbr/RISING_LANDS_BR_.BIN

The existing local BIN/CUE were read only to record identities; no download was
performed. Whole-image hashes are distinct from the extracted CD per-file
inventory hashes:

- BIN: `RISING_LANDS_BR_.BIN`, 705418896 bytes, SHA-256 `c2c09e87927cf5ebbe5d17ea17bffb53c82c2e68385e9259ad0453cc15ea616f`.
- CUE: `RISING_LANDS_BR_.CUE`, 210 bytes, SHA-256 `766fbc02932e3f0454d411211991016142fd361930fc51528fe858fcbf738873`.
- CD inventory:626 files /464,022,464 bytes; source-inventory.json SHA-256
  `d5057f3fae7f24d87e423856040962fdd09fbe4e80b9a0905726e9bbc7340211`. Selected143 game-resource sources
  cover runtime/campaign/shell data; installer/platform binaries are excluded
  explicitly. The BIN hash is not the CD-tree hash.

Extractor source repository:
https://github.com/marciobarbato/rising-lands-reverse-engineering

Extractor commit: `4eb88f23b7b6c03bf1fcfcfee85ee5d53a5f548e`; file:
`assets/extract_assets.py`, SHA-256 `145197a10d2b75e1d0f4d667d606d0068c964e079c172cbcb532499f6db4dc93`.
The manifest records each exact decoder module/commit/hash and source range.

Release tag: `v1-4eb88f2` (immutable annotated tag). The tag's target commit and
manifest hash are pinned by assets/ORIGIN.json in the code repository, avoiding
a circular self-commit field in this release.

See [manifest](manifest.json), [formats](FORMAT.md), [handoff](HANDOFF.md),
[source inventory](source-inventory.json) and [validation](validation.json).
Payload paths resolve under manifest content_root (`data`). All payload files
are at most32MiB; split originals have whole-source reassembly proofs.

The pack preserves opaque PIE/LZS/FNT/video/COL/MAP resources without claiming
semantic decoding. One PCM16 native output has an explicit1-byte incomplete
frame tail; no padding or bytes were dropped. No milestone, game behavior or
real-time device validation is claimed.

Historical first-generation extractor: `12889765a00404a96d92e4483f71cb1b91debd4b`.
That SHA is retained for provenance only; reproduction uses the reachable new
`4eb88f23b7b6c03bf1fcfcfee85ee5d53a5f548e` tooling commit, so deletion of the
old code payload branch does not remove the required implementation.
