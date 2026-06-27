# open-songbook (private dataset)

A git-backed, plaintext dataset of chord sheets / lead sheets backing the
Songbook app's search. **Private** repo — not for public redistribution. See the
main app's `DATASET-PLAN.md` / `DATASET-PHASE1.md` for the design.

## Layout

```
songs/<shard>/<workId>/work.json          # work-level metadata + canonical pick
songs/<shard>/<workId>/<arrangementId>.chopro|.abc   # one arrangement per file
index/index.ndjson                         # GENERATED search index (do not hand-edit)
schema/song.schema.json                    # frontmatter schema + schemaVersion
```

- **work** = a composition (`workId = slugify(normalize(artist)-normalize(title))`).
- **arrangement** = a specific chord sheet for a work. Source-imported ids are
  `ug-<id>` / `session-<id>` (so re-imports dedupe); otherwise content-hashed
  `h-<sha1(normalizedContent)[:8]>`.
- Each arrangement file = YAML frontmatter (provenance: workId, arrangementId,
  source, sourceUrl, variant, key, contributedAt, schemaVersion) + the unchanged
  ChordPro/ABC body.
- `index/index.ndjson` carries only search fields, regenerated from the files.

## Provenance

Every entry stores `source` / `sourceUrl` / `contributedAt` / `schemaVersion` so
the collection can be audited (and, if ever made public, takedown-managed)
without a rewrite.

## Regenerating

The app server owns this checkout. Seed/refresh + index rebuild happen via the
main repo's `scripts/build-dataset-seed.ts` and the `open-songbook-sync` timer.
