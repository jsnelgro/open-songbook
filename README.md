# open-songbook

A plaintext dataset of chord sheets / lead sheets in Chordpro and ABC formats.

## Layout (WIP)

```
songs/<shard>/<workId>/work.json          # work-level metadata + canonical pick
songs/<shard>/<workId>/<arrangementId>.chopro|.abc   # one arrangement per file
index/index.ndjson                         # GENERATED search index (do not hand-edit)
schema/song.schema.json                    # frontmatter schema + schemaVersion
```

- Each arrangement file = YAML frontmatter (provenance: workId, arrangementId,
  source, sourceUrl, variant, key, contributedAt, schemaVersion) + the unchanged
  ChordPro/ABC body.
- `index/index.ndjson` carries only search fields, regenerated from the files.
