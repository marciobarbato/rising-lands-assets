# Extracted asset formats v1

Payload paths resolve relative to the manifest's content_root (data). There
are no timestamps, absolute source paths, platform-dependent encoders or labels
inferred from gameplay. Source names and game text retain original spelling.

- graphics/BANK/indices.u8 and opacity.u8 concatenate row-major frames. Both
  planes have identical dimensions/offsets from frames.json. Indices are u8;
  masks are0 for transparent skip and 255 for opaque. Literal index0 can be
  opaque. No RGB conversion or guessed background is applied. frames.json maps
  every decoded range to the original header and compressed source range and
  records both plane hashes. Anchors/clipping are not encoded in CMP; renderer
  metadata must supply them, never invented defaults.
- palettes/NAME.rgb8 is256 RGB triplets,8-bit, from the exact unchanged native
  LoadPalette reconstruction: VGA component<<2 (max252), entry0 black. This
  byte transform is distinct from the obsolete Core +3 reader. Palette cycling
  and live shadow/remap are not assets exported here.
- audio/BANK/INDEX-vVARIANT.wav is uncompressed RIFF WAVE PCM, preserving the
  original channels, sample rate and sample bits. Its data chunk is only the
  native decoder's written prefix. Unwritten fixture fill is excluded. The
  manifest includes whole native buffer hashes checked against frozen captures,
  written-byte hashes and SND payload/HED header/index offsets. samples.json
  contains IDs/variants/format only; speaker/event names are not invented.
- audio/BANK/header.hex.json is a reversible exact byte transport of HED, not
  a new semantic bank decoder. The native bank reader remains authoritative.
- worlds/SOURCE.json is canonical JSON from unchanged formatos.ler_eta.
  Parsed fields retain their established names and unknown tables stay unnamed.
  Complete original world bytes are also preserved, because this JSON omits
  inactive map cells and uninterpreted suffix bytes. The suffix is not silently
  discarded or assigned gameplay meaning.
- text/SOURCE.utf8.txt is a reversible Latin1-byte-to-UTF8 mapping. CR/LF and
  every original byte are recoverable. This transport does not assert which
  Windows code page the game used or change player-visible Portuguese wording.
- preserved/SOURCE.part-NNNN.bin is an exact original source slice at the
  manifest offset. Concatenating parts in source-offset order reproduces the
  whole source hash. Payloads are at most32MiB. PIE/LZS pictures, FNT glyphs,
  FLC/AVI frames and other unproved binary structures are explicitly opaque;
  preserving their bytes does not count as decoding their semantic content.

Source CMP/SND files are not duplicated merely to retain compression choices:
all their decoded outputs equal the validated reader bytes, and the complete
original source identities are pinned. Original complete world/picture/font/
video bytes are retained only where unknown content would otherwise be lost.

A real exception is P/index221/variant0: the native PCM16 mono output is291,939
bytes, ending in one incomplete sample byte. Its WAV contains 291,938 complete
PCM bytes; a separate1-byte incomplete-frame-tail.bin preserves the remainder.
WAV data plus that sidecar equals the exact native-written output and its hash.
No padding, dropped byte or fabricated sample is used. This tail is an explicit
format boundary, not audible/real-device playback validation.
