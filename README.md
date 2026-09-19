# RRL trail anchors

Once a day, [RRL](https://rrl.syfers.eu) writes one line here: the heads of its data trail. The line holds no project content, names or ids, and nothing here is ever changed or removed.

Each file `anchors/YYYY/MM/DD.json` holds:

| Field | Meaning |
|---|---|
| `date` | the day anchored |
| `at` | the moment of anchoring (UTC) |
| `auditSeq` | position of the last audit row at that moment |
| `auditHead` | hash of that audit row (SHA-256, hex) |
| `root` | SHA-256 over the sorted latest revision hashes of all projects |

## Checking a project's trail

A steward, observer or platform admin can export a project's trail from RRL (JSON). Anyone can then check it without RRL:

```
node scripts/verify-trail.mjs <export.json> --public syntrociety/rrl-trail-anchors
```

The script is in the RRL repository. It recomputes both hash chains, the revisions and the audit log, and compares every anchor in the export with the line published here. Commits are made through the GitHub API and signed by GitHub, and this branch refuses force pushes and deletion.

Background: RFC-009 and ADR-014 in the RRL repository.
