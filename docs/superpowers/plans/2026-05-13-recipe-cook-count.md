# Recipe Cook Count Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Add a Meta Bind powered "做过一次" button to recipe notes so each recipe tracks how many times it has been cooked.

**Architecture:** Store the count directly in each recipe's frontmatter as `做过次数`. Render the count and increment button near the recipe title using Meta Bind inline view and button syntax, with the button updating only the current note.

**Tech Stack:** Obsidian Markdown, YAML frontmatter, Meta Bind `VIEW`, `BUTTON`, and `updateMetadata`.

---

### Task 1: Add Cook Count To Recipe Template

**Files:**
- Modify: `00 模板/菜谱模板.md`

- [x] **Step 1: Add the frontmatter field**

Add `做过次数: 0` after `难度:` in the YAML block:

```yaml
难度:
做过次数: 0
主料标签:
```

- [x] **Step 2: Add the visible count and button call**

Add this directly below `# {{菜名}}`:

```markdown
做过：`VIEW[{做过次数}]` 次 `BUTTON[recipe-cooked-once]`
```

- [x] **Step 3: Add the hidden Meta Bind button definition**

Add this below the visible count line:

````markdown
```meta-bind-button
label: "做过一次"
hidden: true
id: "recipe-cooked-once"
style: primary
actions:
  - type: updateMetadata
    bindTarget: 做过次数
    evaluate: true
    value: "x + 1"
```
````

- [x] **Step 4: Verify the template syntax**

Run:

```bash
sed -n '1,80p' '00 模板/菜谱模板.md'
```

Expected: the file contains `做过次数: 0`, the visible `VIEW`/`BUTTON` line, and one `meta-bind-button` code block.

### Task 2: Add Cook Count To Existing Recipes

**Files:**
- Modify: `01 菜谱/可乐鸡翅.md`
- Modify: `01 菜谱/重庆烤鱼（真鯛版）.md`

- [x] **Step 1: Add the frontmatter field to each existing recipe**

Add `做过次数: 0` after `难度:` in each recipe:

```yaml
难度: 简单
做过次数: 0
主料标签:
```

For the roasted fish recipe:

```yaml
难度: 中等
做过次数: 0
主料标签:
```

- [x] **Step 2: Add the visible count and button call to each existing recipe**

Add this directly below each `# 菜名` heading:

```markdown
做过：`VIEW[{做过次数}]` 次 `BUTTON[recipe-cooked-once]`
```

- [x] **Step 3: Add the hidden Meta Bind button definition to each existing recipe**

Add this below the visible count line in each recipe:

````markdown
```meta-bind-button
label: "做过一次"
hidden: true
id: "recipe-cooked-once"
style: primary
actions:
  - type: updateMetadata
    bindTarget: 做过次数
    evaluate: true
    value: "x + 1"
```
````

- [x] **Step 4: Verify all recipe files contain the expected fields and button blocks**

Run:

```bash
rg -n "做过次数|recipe-cooked-once|meta-bind-button|VIEW\\[\\{做过次数\\}\\]" '00 模板' '01 菜谱'
```

Expected: each of the template and two recipe files has one `做过次数: 0`, one visible `VIEW[{做过次数}]` line, and one `recipe-cooked-once` button definition.

### Task 3: Final Validation And Commit

**Files:**
- Verify: `00 模板/菜谱模板.md`
- Verify: `01 菜谱/可乐鸡翅.md`
- Verify: `01 菜谱/重庆烤鱼（真鯛版）.md`

- [x] **Step 1: Check for unrelated changes**

Run:

```bash
git status --short
```

Expected: only the plan file, recipe template, and two recipe notes are modified or added.

- [x] **Step 2: Review the diff**

Run:

```bash
git diff -- '00 模板/菜谱模板.md' '01 菜谱/可乐鸡翅.md' '01 菜谱/重庆烤鱼（真鯛版）.md' docs/superpowers/plans/2026-05-13-recipe-cook-count.md
```

Expected: diff only adds the cook-count frontmatter, visible Meta Bind line, hidden button block, and this implementation plan.

- [x] **Step 3: Commit the implementation**

Run:

```bash
git add docs/superpowers/plans/2026-05-13-recipe-cook-count.md '00 模板/菜谱模板.md' '01 菜谱/可乐鸡翅.md' '01 菜谱/重庆烤鱼（真鯛版）.md'
git commit -m "feat: add recipe cook counter"
```
