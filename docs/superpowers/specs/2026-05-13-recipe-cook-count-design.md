# Recipe Cook Count Design

## Goal

Add a lightweight "cooked count" affordance to every recipe note so we can track how many times a recipe has been made.

## Scope

- Store the count in recipe frontmatter as `做过次数`.
- Show the current count near the top of each recipe body.
- Add a Meta Bind button that increments `做过次数` by 1 in the current note.
- Keep the design intentionally small: no cook-date log, no ratings, and no separate statistics note in this iteration.

## Data Model

Each recipe note should include:

```yaml
做过次数: 0
```

The field is numeric and defaults to `0` for new recipes and existing recipes that have not been cooked yet.

## Interaction

Near the recipe title, each note should show the current count and a one-click button:

```markdown
做过：`VIEW[{做过次数}]` 次 `BUTTON[recipe-cooked-once]`
```

The button is defined in the same note with Meta Bind's `updateMetadata` action:

```yaml
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

## Files To Update During Implementation

- `00 模板/菜谱模板.md`
- Existing notes under `01 菜谱/`

## Error Handling

- Existing recipes start at `0`, avoiding an undefined `x` value when the button is clicked.
- The field name stays consistent across the template and existing notes.
- The button only updates the current note's frontmatter, not other recipe files.

## Testing

- Confirm each edited recipe has `做过次数: 0` in frontmatter.
- Confirm each edited recipe includes the Meta Bind button block and the visible count/button line.
- In Obsidian, open one recipe and click the button once to verify the frontmatter changes from `0` to `1`.
