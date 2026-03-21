# heatedhornet

Canonical store list, published to the Buf Schema Registry at buf.build/gkwa/heatedhornet.

Defines a StoreId protobuf enum where each value carries its display name as a custom option.
Display names (with apostrophes, punctuation, etc.) are embedded directly in the schema so
consumers get the correct strings via protobuf reflection with no hand-written mapping table.

## adding a store

1. Add a new enum value to stores/v1/stores.proto with a display_name option
2. git commit
3. buf push

## consumers

- github.com/taylormonacelli/itshire
- github.com/taylormonacelli/rainbowrooster

Both consume the store list by running buf generate against this module and reading
display names via reflection at runtime.

## development

```bash
buf lint
buf breaking stores/v1/stores.proto --against buf.build/gkwa/heatedhornet
buf push
```
