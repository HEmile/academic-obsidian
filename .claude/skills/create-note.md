---
description: "Create a new note in the vault — paper, topic, concept, author, institution, venue, project, or idea with proper frontmatter and tags"
---

# Create Note

Create a new markdown note following the vault's conventions exactly.

## General Rules

- File goes in the **root directory** (not in any subfolder)
- Filename = the note's primary name (no prefixes, IDs, or special formatting)
- Tags go at the **end** of the file after a `---` separator, NOT in YAML frontmatter
- Wikilinks in frontmatter must be quoted: `"[[Name]]"`
- The `Created` field uses format: `"[[DD-MM-YYYY]]"` (today's date)
- Aliases should be a YAML list
- Do NOT auto-create notes for any `[[wikilinks]]` that don't resolve — leave them as unresolved
- Body text between frontmatter and tags is for the user's own notes — leave it empty or add minimal content as requested

## Templates by Type

### Paper (`#source/paper`)
```yaml
---
aliases:
  - citekey or acronym
year: YYYY
hasTopic:
  - "[[topic]]"
author:
  - "[[Author Name]]"
project:
publishedIn: "[[Venue]]"
citeKey:
zoteroUri:
url:
Created: "[[DD-MM-YYYY]]"
---

(body text — user's notes about the paper)

---
#source/paper
```

### Topic (`#topic`)
```yaml
---
aliases: []
subset:
  - "[[parent topic]]"
Created: "[[DD-MM-YYYY]]"
---

(body text)

---
#topic
```

### Concept (`#concept`)
```yaml
---
aliases: []
hasTopic:
  - "[[related topic]]"
isA:
  - "[[parent concept]]"
Created: "[[DD-MM-YYYY]]"
---

(body text)

---
#concept
```

### Author (`#author #topic`)
```yaml
---
worksIn:
  - "[[Institution]]"
Created: "[[DD-MM-YYYY]]"
---

---
#author #topic
```

### Institution (`#institution #topic`)
```yaml
---
aliases:
  - abbreviation
partOf: "[[parent institution]]"
---

---
#institution #topic
```

### Venue — Conference (`#venue/conference #topic`)
```yaml
---
aliases:
  - abbreviation
---

---
#venue/conference #topic
```

### Venue — Journal (`#venue/journal #topic`)
```yaml
---
aliases:
  - abbreviation
---

---
#venue/journal #topic
```

### Project (`#project`)
```yaml
---
aliases: []
with:
  - "[[Collaborator]]"
hasTopic:
  - "[[topic]]"
Created: "[[DD-MM-YYYY]]"
---

(body text)

---
#project
```

### Project Idea (`#project/idea`)
```yaml
---
with: "[[Collaborator]]"
hasTopic: "[[topic]]"
score: 3
Created: "[[DD-MM-YYYY]]"
---

(body text)

---
#project/idea
```

### Talk (`#source/talk`)
```yaml
---
aliases: []
by:
  - "[[Speaker]]"
at:
  - "[[Venue]]"
hasTopic:
  - "[[topic]]"
year: YYYY
Created: "[[DD-MM-YYYY]]"
---

(body text)

---
#source/talk
```

### Method (`#method`)
```yaml
---
aliases:
  - abbreviation
isA: "[[parent method]]"
Created: "[[DD-MM-YYYY]]"
---

(body text)

---
#method
```
