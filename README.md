# Bible translations

Offline scripture databases downloaded on demand by a private Android Bible
reader. This repository holds data only, with no app code. Each file is a
gzip-compressed SQLite database attached to a release: `v2` for the app from
version 1.2.0, and `v1` for 1.0 and 1.1, which pin its files and keep using them.

The app pins the exact size and SHA-256 of every file it will accept. A file
that does not match is discarded, so these assets must never be replaced in
place. A corrected text becomes a new release with a new app build.

| File | Translation | Year | Compressed | SHA-256 (compressed file) |
| --- | --- | --- | --- | --- |
| `bible_web.db.gz` | World English Bible | 2020 | 1,534,096 bytes | `fff2ea02edbb2f56e81564847d6331f08d0b57d708c1b211ac197b1925b4993a` |
| `bible_asv.db.gz` | American Standard Version | 1901 | 1,583,270 bytes | `da4c6f5b8dd63a7bd42cdbdcede08cfec0b9632d01d9368ca7806966f58d6317` |
| `bible_ylt.db.gz` | Young's Literal Translation | 1898 | 1,609,266 bytes | `13ae2524f1ea0311528e248a8840347435871dfc8df6da57418056ebb9f49cfe` |
| `bible_bbe.db.gz` | Bible in Basic English | 1965 | 1,510,585 bytes | `a9d49696a6944ac4fa72579134e4601728771837a97c372948ee15e812444013` |

The table is `v2`. It differs from `v1` only in the World English Bible, which
eBible.org revised in September 2026: five verses of Daniel (4:26, 9:11, 11:20,
11:21, 11:24). The other three files are byte for byte the same in both. `v1`'s
`bible_web.db.gz` is 1,534,103 bytes, SHA-256
`5b3e6d60e60c3f49e002bc27e584943e618709c15fb4560eea43f9f6da851948`.

Each release's files are also committed in a folder of the same name (`v1/`,
`v2/`), so they can be
served by the jsDelivr CDN as a fallback where github.com cannot be reached. The
app pins that fallback to a specific commit, and checks the size and SHA-256 of
whatever it downloads from either place.

`manifest.json` lists the same files with the uncompressed database sizes and
hashes the app checks after decompressing. It also describes the texts built into
the app and not hosted here: the King James Version and, from `v2`, the app's
own Lithuanian New Testament, a draft translated from the Greek.

## Sources and licences

All four texts come from [eBible.org](https://ebible.org) and are distributed
there as public domain. The words are unchanged. Only the markup is converted:
verse and paragraph structure, Psalm titles, and square brackets. Brackets
around words the translators supplied become italics; brackets that mark a
disputed passage, or that are left unclosed in the source, are removed.

- **World English Bible** (`engwebp`). Public domain. "World English Bible" is a
  trademark of eBible.org, and the name may only be used for unaltered text.
- **American Standard Version** (`eng-asv`). Public domain.
- **Young's Literal Translation** (`engylt`). Public domain.
- **Bible in Basic English** (`engBBE`). Public domain in the United States.
  eBible.org notes it was printed in 1965 without a copyright notice. Its status
  may differ in other countries.

No copyrighted translation (NIV, ESV, NASB, NKJV, CSB and others) is, or will
be, hosted here.

## Schema

Each database has `book` and `verse` tables plus a `meta` table naming the
translation, its source and its licence. Footnotes and cross-references are not
included. Empty verses are deliberate: they mark verses that a critical text
omits (for example Acts 8:37 in the WEB, ASV and BBE), which keeps every
translation aligned to the same verse numbers.
