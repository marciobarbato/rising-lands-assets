# External original-data release handoff

Data repository: https://github.com/marciobarbato/rising-lands-assets.git
Release: immutable annotated tag v1-4eb88f2. This publication extends existing
main7256128 (README history), with a normal main push separately authorized by
the user. It does not merge any old code-repository payload history.

## Extractor and reproduction

The reachable tooling implementation is code commit
4eb88f23b7b6c03bf1fcfcfee85ee5d53a5f548e in
https://github.com/marciobarbato/rising-lands-reverse-engineering.git,
assets/extract_assets.py. Its file SHA is recorded in README/validation.json.
The earlier extractor12889765a00404a96d92e4483f71cb1b91debd4b is historical
provenance only and is not needed to reproduce this release. All761 payload
bytes match that approved earlier pack; the root manifest now references the
root source inventory and the new reachable tooling commit.

The code branch feat/codex-assets-tooling adds ORIGIN only after this data
commit/tag is published. This avoids circular commit references. ORIGIN pins
repository, commit, annotated-tag object, manifest and inventory SHA-256.
From a code checkout containing that pin, verify a clean checkout of this
release with the original CD supplied read-only:

```sh
python3 -B assets/extract_assets.py \
  --cd-root '/Users/marcio/git/Rising Lands/source/cd' \
  --data-root /absolute/path/to/rising-lands-assets --check
python3 -B -m unittest discover -s assets/testes -v
```

Verification checks the pin before/after fresh regeneration of every payload
and root-manifest byte. Wrong/missing/modified inputs fail; no auto-fetch,
branch switch, fallback or repair occurs. No tool writes into this pinned data
checkout. Logs are kept outside it. The source-inventory metadata lives only
here, rather than being copied back into code history.

## Counts, identities and proof

Inventory:626 original CD files,143 selected resources,483 explicit exclusions.
Payloads:761;12,268 frames in8 CMP banks,7 palettes,551 WAVs and1 one-byte
incomplete-frame sidecar,43 structured worlds,33 reversible text files,96
original preserved sources in98 parts. The43 worlds are38 MONDE*.ETA files
plus ALIBABA/CHAMPS/CIRQUE/CRANE/MASSIF.NET. No exact per-mission/event
reachability is inferred. FORMAT.md specifies the lossless layouts.

Payload size629,204,621 bytes; the root manifest size/hash and all full
source/output hashes are in validation.json/manifest.json. Each file is at most
33,554,432 bytes (32MiB), below the50MB cap. Split parts are reassembled and
checked against whole-source identities. The manifest records source ranges
and each decoder's module, commit and file hash.

All551 existing original complete-audio-buffer hashes match. The export retains
48,945,219 native-written audio bytes and excludes334,880 inherited/unwritten
fixture bytes. P/index221/variant0 is the explicit PCM16 alignment boundary:
291,938 complete WAV bytes plus1 preserved byte reproduce all291,939 written
bytes; no sample padding or truncation is invented.

Generation used the unchanged committed native Python readers; it executed no
original x86. Sixteen tooling tests cover byte transport, opaque literal-zero
masks, WAV/tail identity, output/source boundaries and fail-closed release pins.
No decoder, renderer, game behavior, real-time sound device or milestone is
implemented by this data publication.

The exact Internet Archive URL was supplied by the user and is recorded in
README. The existing BIN/CUE hashes were read locally and are distinct from
CD-tree inventory identities. No new download was performed.

## Remaining boundaries and historical branch

PIE/LZS picture pixels, FNT glyph layout, FLC/AVI frames and COL/MAP semantics
remain explicit decoder gaps. Their bytes are preserved losslessly, not counted
as semantic decodes. Anchors/clipping, executable-resident resources, original
Windows code-page interpretation and app/Rust bundling remain separate work.

The historical feat/codex-assets branch and old independent clone are preserved.
After the coordinator fetches this immutable release, verifies its contents
through the pinned tooling and retains the reachable new tooling implementation,
the coordinator may delete the old remote branch. This front does not delete
it, force-push or rewrite code main/history. Old payload commits are absent
from the new code-tooling branch and clone.
