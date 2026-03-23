---
description: "Query the academic Obsidian vault — answer questions about papers, authors, topics, concepts, and their relationships"
---

# Query Vault

Answer natural language questions about the vault's knowledge graph by translating them into file searches.

## Strategy

1. **Identify the query type** from the user's question
2. **Search broadly first** — use case-insensitive grep across filenames and aliases
3. **Read matching files** to extract structured data from frontmatter and body
4. **Follow links** for multi-hop queries (e.g., author → papers → topics)
5. **Present results** with `[[wikilinks]]` so the user can click through in Obsidian

## Query Type Decision Tree

### "What papers are about X?"
1. Find the topic/concept note for X (search by filename and aliases)
2. Grep for papers with X in `hasTopic`: `grep -l "hasTopic:" *.md | xargs grep -l "[[X]]"`
3. Also search body text: `grep -rl "\[\[X\]\]" *.md` filtered to `#source/paper` files
4. For each paper found, extract: title, year, authors, venue

### "Who wrote paper X?"
1. Find the paper file by name or alias
2. Read its `author:` frontmatter field
3. Return the list of `[[Author]]` links

### "What does author X work on?"
1. Find all papers where X appears in `author:` field
2. Collect all `hasTopic` values from those papers
3. Deduplicate and present as a topic list

### "What is X?" / "Tell me about X"
1. Find the note by filename or alias (case-insensitive)
2. Read the full file — frontmatter for metadata, body for the user's notes
3. Present a summary including type, relationships, and body content

### "What papers did X publish at venue Y?"
1. Find papers with X in `author:` AND Y in `publishedIn:`
2. Chain grep: `grep -l "author:" *.md | xargs grep -l "[[X]]" | xargs grep -l "[[Y]]"`

### "Who at institution X works on topic Y?"
Multi-hop query:
1. Find authors with X in `worksIn:`
2. For each author, find their papers
3. Check if any paper has Y in `hasTopic:`
4. Return matching authors

## Alias-Aware Search

Many notes are referenced by aliases (e.g., "NeSy" for "neurosymbolic AI", "DFL" for "Analyzing differentiable fuzzy logic operators"). Always:
1. First try exact filename match
2. If no match, grep for the term in `aliases:` blocks: `grep -B1 -A10 "^aliases:" *.md | grep -il "search term"`
3. Once you find the canonical note, use its filename for further queries

## Output Format

- Use `[[wikilinks]]` for all note references
- For paper lists: include year, authors, and venue when available
- For broad queries: use judgment on verbosity — exhaustive for specific queries (e.g., "papers by X"), concise summaries for broad ones (e.g., "what do we know about deep learning?")
- Group results logically (by topic, by year, by author) when there are many

## Example

**User**: "What papers in the vault discuss fuzzy logic?"

**Agent approach**:
1. `grep -rl "\[\[fuzzy logic\]\]" *.md` to find all mentions
2. Filter results to files tagged `#source/paper`
3. Read each paper's frontmatter for year/author/venue
4. Present sorted by year
