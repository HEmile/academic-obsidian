---
description: "Build a research profile for an author — their affiliation, papers, research areas, co-authors, and projects"
---

# Author Profile

Compile everything the vault knows about a researcher by chaining frontmatter lookups.

## Strategy

### Step 1: Find the author note
Search by name and aliases (case-insensitive). Read the full note.

### Step 2: Extract affiliation
Read the `worksIn:` field for institutional links.

### Step 3: Find all papers by this author
```bash
grep -l "author:" *.md | xargs grep -l "\[\[Author Name\]\]"
```
For each paper, extract: title, year, hasTopic, publishedIn, co-authors.

### Step 4: Derive research areas
Collect all unique `hasTopic` values from the author's papers. Rank by frequency.

### Step 5: Find co-author network
From the papers found in Step 3, collect all other authors. Rank by co-authorship frequency.

### Step 6: Find projects and ideas
```bash
grep -l "with:" *.md | xargs grep -l "\[\[Author Name\]\]"
```
Filter to `#project` and `#project/idea` files.

### Step 7: Check for talks
```bash
grep -l "by:" *.md | xargs grep -l "\[\[Author Name\]\]"
```
Filter to `#source/talk` files.

## Output Format

```markdown
## [[Author Name]]

**Affiliation**: [[Institution]]

### Papers in Vault (N total)
- **[[Paper Title]]** (Year) — with [[Co-author1]], [[Co-author2]]. In [[Venue]].
- ...

### Research Areas
- [[Topic 1]] (N papers)
- [[Topic 2]] (N papers)
- ...

### Frequent Co-authors
- [[Co-author A]] (N papers together)
- ...

### Projects
- [[Project Name]] — topics: ...

### Talks
- [[Talk Title]] (Year) at [[Venue]]
```

Sort papers by year (newest first). Only include sections that have content.
