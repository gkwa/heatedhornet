# heatedhornet

Canonical store list, published to the Buf Schema Registry at buf.build/gkwa/heatedhornet.

Defines a StoreId protobuf enum where each value carries its display name as a custom option.
Display names (with apostrophes, punctuation, etc.) are embedded directly in the schema so
consumers get the correct strings via protobuf reflection with no hand-written mapping table.

## adding a store

Adding a store involves more than editing this repo — all consumers must be updated
and the Obsidian plugin must be rebuilt or the Shopping list breaks.

Follow the full runbook in the Obsidian vault: "adding a new store.md"

Key rules:
- Display names must not contain parentheses — Obsidian Bases treats `name_(part)`
  as a function call in formulas, breaking all Shopping list views
- Steps: edit proto → push to GitHub + BSR → buf generate in each consumer →
  reinstall itshire → run rainbowrooster → run itshire → rebuild iridecentibis plugin

## consumers

- github.com/taylormonacelli/itshire (Python, adds store sections to vault product files)
- github.com/taylormonacelli/rainbowrooster (Python, generates product frontmatter + Shopping list.base)
- github.com/taylormonacelli/iridecentibis (TypeScript Obsidian plugin, implements grocery-check view)

## development

```bash
buf lint
buf breaking stores/v1/stores.proto --against buf.build/gkwa/heatedhornet
buf push
```
