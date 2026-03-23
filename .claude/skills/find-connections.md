---
description: "Discover how two notes are connected — find shared topics, authors, projects, and paths through the knowledge graph"
---

# Find Connections

Given two notes (papers, topics, authors, concepts, etc.), discover how they relate through the knowledge graph. This is a "six degrees of separation" explorer.

## Strategy

### Step 1: Identify both notes
Find notes A and B by name or alias. Read both fully to understand their type and metadata.

### Step 2: Check direct links
- Does A's body or frontmatter link to B? (`grep "\[\[B\]\]" "A.md"`)
- Does B's body or frontmatter link to A?
- If yes → direct connection found.

### Step 3: Check shared properties
Depending on note types, check for overlap:

| If A and B are both... | Check for shared... |
|------------------------|-------------------|
| Papers | authors, topics, venues, projects |
| Topics | parent topics (subset), papers that cover both |
| Authors | co-authored papers, institutions, topics they publish on |
| Paper + Topic | does the paper have this topic? |
| Paper + Author | is the author on this paper? |
| Author + Institution | does the author work there? |

### Step 4: Find graph paths (if no direct/shared connection)
Try 2-hop paths:
- A → (some intermediate note) → B
- For papers: A shares an author with paper C, which shares a topic with B
- For topics: A is a subtopic of X, which is also a parent of B
- For authors: A co-authored with C, who co-authored with B

### Step 5: Check body text mentions
Search both files' body text for mentions of each other or shared terms.

## Output Format

Present connections from strongest to weakest:

```markdown
## Connections between [[A]] and [[B]]

### Direct Links
- A links to B via `hasTopic` field

### Shared Properties
- Both are about: [[topic1]], [[topic2]]
- Shared authors: [[Author X]]

### Through the Graph
- A → [[Author X]] → B (Author X wrote both papers)
- A → [[Topic Y]] → B (both relate to Topic Y)

### Mentions
- A's body text mentions "term" which is an alias of B
```

## Example

**User**: "How are fuzzy logic and neurosymbolic AI related?"

**Agent approach**:
1. Read both topic notes
2. Check if either's `subset` references the other
3. Find papers that have both in `hasTopic`
4. Check if one is a subtopic ancestor of the other
5. Present the connections
