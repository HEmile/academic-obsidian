# Academic Obsidian Vault

This is a flat-structure academic knowledge graph. All notes live in the root directory — no folder hierarchy. Notes are linked via YAML frontmatter (typed links) and wikilinks in body text.

## Note Types

| Type | Tag (end of file) | Frontmatter fields |
|------|-------------------|-------------------|
| Paper | `#source/paper` | aliases, author, hasTopic, project, publishedIn, year, citeKey, zoteroUri, url |
| Talk | `#source/talk` | aliases, by, at, hasTopic, year, Created |
| Topic | `#topic` | aliases, subset, Created |
| Concept | `#concept` | aliases, hasTopic, isA, Created |
| Method | `#method` | aliases, isA, Created |
| Author | `#author #topic` | worksIn, Created |
| Institution | `#institution #topic` | aliases, partOf |
| Venue (conf) | `#venue/conference #topic` | aliases |
| Venue (journal) | `#venue/journal #topic` | aliases |
| Project | `#project` | aliases, with, hasTopic, Created |
| Project Idea | `#project/idea` | with, hasTopic, score, Created |

## Conventions

- **Tags** appear at the **end** of the file after a `---` separator, not in YAML frontmatter
- **Wikilinks in frontmatter** are quoted: `"[[Name]]"` or `"[[target|display text]]"`
- **Wikilinks in body text** are unquoted: `[[Name]]`
- **Dates** use `"[[DD-MM-YYYY]]"` format in the `Created` field
- **Aliases** are YAML lists of alternative names (acronyms, citekeys, etc.)
- **subset** on topics forms a DAG of parent topics (not a strict tree)
- **isA** on concepts forms a type hierarchy
- Files in `Templates/`, `Bases/`, `Files/`, `.obsidian/` are Obsidian internals — do not modify

## Key Relationships

```
Paper  --author-->      Author  --worksIn-->  Institution
Paper  --hasTopic-->    Topic   --subset-->   Topic (parent)
Paper  --publishedIn--> Venue
Paper  --project-->     Project --with-->     Author
Concept --hasTopic-->   Topic
Concept --isA-->        Concept (parent)
```

## Query Patterns

```bash
# Find all notes of a type (tag is on its own line near end of file):
grep -l "#source/paper" *.md
grep -l "#topic" *.md
grep -l "#concept" *.md
grep -l "#author" *.md

# Find papers on a topic:
grep -l "hasTopic:" *.md | xargs grep -l "fuzzy logic"

# Find papers by an author:
grep -l "author:" *.md | xargs grep -l "Emile van Krieken"

# Find backlinks (what links TO a note):
grep -rl "\[\[fuzzy logic\]\]" *.md

# Find topic children (subtopics of X):
grep -l "subset:" *.md | xargs grep -l "\[\[machine learning\]\]"

# Search by alias (case-insensitive):
grep -il "NeSy" *.md
```

## Rules

- Never auto-create notes for unresolved wikilinks — leave them as-is
- Never summarize papers or import bibtex — the user has Obsidian plugins for that
- Always search by both filename AND aliases (case-insensitive)
- When creating notes, follow the templates in `Templates/` exactly
