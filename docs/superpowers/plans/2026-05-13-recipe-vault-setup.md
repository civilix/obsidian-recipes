# Recipe Vault Setup Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create the first-pass Obsidian recipe vault structure, a unified recipe template, and an AI import prompt optimized for mobile reading and structured ingredient extraction.

**Architecture:** Use a minimal folder layout with one canonical recipe template and one canonical AI import prompt. Keep recipe metadata small and store detailed ingredient quantities in body sections so notes stay readable on mobile while still supporting future ingredient-based recommendations.

**Tech Stack:** Markdown, Obsidian vault conventions, Git

---

### Task 1: Add design and usage documentation

**Files:**
- Create: `docs/superpowers/specs/2026-05-13-recipe-vault-design.md`
- Create: `docs/superpowers/plans/2026-05-13-recipe-vault-setup.md`
- Create: `README.md`

- [ ] **Step 1: Write the design spec**

Add a spec that records the approved decisions: mobile-first reading order, one unified template, one primary cooking method, and `主料标签` as the future recommendation signal.

- [ ] **Step 2: Add a short README**

Describe the initial folder layout and explain the purpose of each top-level folder in plain language.

- [ ] **Step 3: Review the docs for consistency**

Check that the README, spec, and plan all describe the same folder layout and property names.

- [ ] **Step 4: Commit**

```bash
git add docs/superpowers/specs/2026-05-13-recipe-vault-design.md docs/superpowers/plans/2026-05-13-recipe-vault-setup.md README.md
git commit -m "docs: add recipe vault design and setup plan"
```

### Task 2: Create the initial vault structure

**Files:**
- Create: `00 模板/菜谱模板.md`
- Create: `01 菜谱/00 说明.md`
- Create: `02 食材/00 说明.md`

- [ ] **Step 1: Create the recipe template**

Add a canonical markdown template with stable frontmatter and a phone-friendly body order:

```md
---
type: recipe
烹饪方式:
份量:
总时长:
难度:
主料标签:
  -
来源:
tags:
  - 菜谱
---

# {{菜名}}

## 主料
- 食材名｜用量

## 辅料
- 食材名｜用量

## 调料
- 调料名｜用量

## 步骤
1.

## 备注
- 可替换食材：
- 关键提醒：
- 复热方式：
```

- [ ] **Step 2: Create lightweight folder notes**

Add short notes in `01 菜谱/` and `02 食材/` so the intended purpose of each area is clear inside the vault.

- [ ] **Step 3: Review the template**

Confirm that the body order puts ingredients before steps and that `主料标签` exists in frontmatter for later recommendation workflows.

- [ ] **Step 4: Commit**

```bash
git add '00 模板/菜谱模板.md' '01 菜谱/00 说明.md' '02 食材/00 说明.md'
git commit -m "feat: add initial recipe vault structure"
```

### Task 3: Add the AI import prompt

**Files:**
- Create: `00 模板/AI 导入菜谱提示词.md`

- [ ] **Step 1: Write the import prompt**

Create a reusable prompt that instructs AI to remove filler, preserve key cooking details, split ingredients into `主料` `辅料` `调料`, and output only the final markdown note.

- [ ] **Step 2: Add usage notes**

Explain when to paste raw recipe text or screenshots and remind the user that missing facts should be left blank rather than invented.

- [ ] **Step 3: Review for format stability**

Make sure the prompt enforces one primary cooking method and exact output formatting so repeated imports stay consistent.

- [ ] **Step 4: Commit**

```bash
git add '00 模板/AI 导入菜谱提示词.md'
git commit -m "feat: add recipe import prompt"
```
