---
description: "Explore the topic hierarchy in the vault — find subtopics, parent topics, siblings, and navigate the topic DAG"
---

# Explore Topics

Navigate the vault's topic hierarchy. Topics are linked via the `subset` frontmatter field, forming a directed acyclic graph (DAG) — a topic can have multiple parents.

## Strategy

### Find parent topics of X
1. Find the topic note for X
2. Read its `subset:` field — these are the direct parents
3. Example: `neurosymbolic AI` has subset `["[[machine learning]]", "[[symbolic AI]]"]`

### Find child topics (subtopics) of X
1. Grep for topic notes that list X in their `subset:` field
2. `grep -l "subset:" *.md | xargs grep -l "\[\[X\]\]"` then filter to `#topic` files
3. These are X's direct children

### Find sibling topics
1. Get parents of X (from subset)
2. For each parent, find all children
3. Siblings = children of the same parent, excluding X

### Show full hierarchy around X
1. Get parents (up 1-2 levels)
2. Get children (down 1-2 levels)
3. Render as an indented tree:
```
grandparent
  ├── parent
  │   ├── X ← (you are here)
  │   │   ├── child1
  │   │   └── child2
  │   └── sibling
  └── uncle
```

### Find path between topic A and topic B
1. Walk up from A collecting ancestors
2. Walk up from B collecting ancestors
3. Find the common ancestor (lowest common ancestor in the DAG)
4. Present the path: A → ... → common ancestor → ... → B

## Output Format

- Use `[[wikilinks]]` for all topic references
- Render hierarchies as indented trees with `├──` connectors
- Note when a topic has multiple parents (DAG, not tree)
- Include alias info if it helps clarify what a topic covers

## Example

**User**: "What are the subtopics of logic?"

**Agent approach**:
1. Find all notes where `subset:` contains `[[logic]]`
2. Filter to `#topic` files
3. For each child, optionally find their children too (1 level deeper)
4. Render as a tree
