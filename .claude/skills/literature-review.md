---
description: "Generate a literature review for a research topic — survey all papers, group by subtopic, identify gaps and related projects"
---

# Literature Review

Survey the vault's knowledge about a research area. This produces a structured overview of papers, grouped by subtopic, with the user's own notes and annotations.

## Strategy

1. **Identify the target topic** — find the topic note by name or alias
2. **Find direct papers** — papers with this topic in `hasTopic`
3. **Find subtopics** — topic notes whose `subset` contains the target
4. **Find indirect papers** — papers on those subtopics
5. **Extract metadata** — for each paper: title, year, authors, venue, and the user's body-text notes
6. **Find related projects** — project/idea notes with matching `hasTopic`
7. **Compile and present**

## Detailed Steps

### Step 1: Resolve the topic
```bash
# Find by name or alias
grep -il "search term" *.md
# Confirm it's a topic
grep -l "#topic" <candidates>
```

### Step 2: Direct papers
```bash
grep -l "hasTopic:" *.md | xargs grep -l "\[\[target topic\]\]"
# Filter to #source/paper files
```

### Step 3: Subtopics (one level down)
```bash
grep -l "subset:" *.md | xargs grep -l "\[\[target topic\]\]"
# Filter to #topic files
```

### Step 4: Papers on subtopics
Repeat Step 2 for each subtopic found in Step 3.

### Step 5: Extract per-paper info
Read each paper file and extract:
- **Title**: filename
- **Year**: `year:` field
- **Authors**: `author:` field (list of `[[Author]]` links)
- **Venue**: `publishedIn:` field
- **Notes**: body text between the frontmatter `---` and the closing `---` (before tags)

### Step 6: Related projects
```bash
grep -l "hasTopic:" *.md | xargs grep -l "\[\[target topic\]\]"
# Filter to #project or #project/idea files
```

## Output Format

```markdown
## Literature Review: [[Topic Name]]

### Overview
Brief summary: N papers found, spanning years X–Y, across N subtopics.

### By Subtopic

#### [[Subtopic A]]
- **[[Paper Title]]** (Year) — Authors. Published in Venue.
  > User's notes/summary from the paper file

#### [[Subtopic B]]
...

### Direct Papers (not in a subtopic)
- ...

### Related Projects
- [[Project Name]] — collaborators, score (if idea)

### Gaps
Note any subtopics with few or no papers, or topics referenced but with no papers in the vault.
```

## Guidelines

- Sort papers by year (newest first) within each group
- Include the user's notes verbatim — they wrote them for a reason
- Keep the "Gaps" section honest — it helps the user identify research opportunities
- Use judgment on depth: if there are 50+ papers, summarize rather than listing every one
