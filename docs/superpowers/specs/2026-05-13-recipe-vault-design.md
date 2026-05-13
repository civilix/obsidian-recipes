# Obsidian Recipe Vault Design

**Date:** 2026-05-13

## Goal

Create a mobile-friendly Obsidian recipe vault that is easy for AI to import into and easy for the user to browse while cooking. The structure should also prepare for a future workflow where AI recommends dishes based on currently available ingredients.

## User Constraints

- Primary reading device is a phone.
- Recipes are imported by AI, not typed manually most of the time.
- All recipe notes live together by dish name rather than being split into cooking-method folders.
- Each recipe has one primary cooking method.
- Ingredient-based recommendation should rely mainly on the recipe's core ingredient set.

## Design Decisions

### Vault Structure

- `00 模板/` stores reusable templates and AI prompt references.
- `01 菜谱/` stores recipe notes.
- `02 食材/` is reserved for future ingredient inventory notes.

This keeps the vault simple at the start while leaving a clear place for future inventory tracking.

### Recipe Note Shape

Use one unified recipe template for all cooking methods.

Keep top properties small and stable:

- `type`
- `烹饪方式`
- `份量`
- `总时长`
- `难度`
- `主料标签`
- `来源`
- `tags`

The body order is optimized for phone reading:

1. `主料`
2. `辅料`
3. `调料`
4. `步骤`
5. `备注`

### Ingredient Modeling

Split ingredients into three sections:

- `主料`: ingredients that define what the dish is
- `辅料`: supporting vegetables or side ingredients
- `调料`: seasonings, sauces, spice blends

For future recommendation, only `主料标签` is treated as the main matching signal. Detailed quantities stay in the body for readability.

### AI Import Principles

Imported recipes should:

- remove storytelling, chatter, and repeated filler
- preserve quantities, times, temperatures, and key steps
- choose one primary cooking method
- avoid inventing missing details
- output directly in the vault's standard markdown structure

## Non-Goals

- No method-specific template split yet
- No inventory automation yet
- No Dataview or plugin-driven dashboards yet

## Initial Deliverables

- recipe template file
- AI import prompt file
- lightweight vault structure notes
- short README explaining how the structure works
