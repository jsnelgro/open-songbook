# open-songbook

A directory of plaintext songs in ChordPro and ABC notation.

```
songs/
  ABBA - Dancing Queen.chopro
  Kenny Dorham - Blue Bossa.abc
```

Each file is complete and usable on its own. Metadata stays in the notation:
ChordPro uses `{title:}`, `{artist:}`, and `{key:}` directives; ABC uses normal
`T:`, `C:`, and `K:` headers.

There is no database, generated index, schema, metadata sidecar, or ID hierarchy.
Multiple arrangements simply use readable numbered filenames such as
`Song (2).abc`.
