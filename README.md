# Showcase aliases and custom flags not appearing in explicit_cmd_line field

```
bazel --nohome_rc build --alias=foo --build_event_json_file=bes.json ...; jq 'select(has("optionsParsed"))' bes.json > optionsParsedMsg_alias.json
```

I would expect to see `--alias=foo` inside of the optionsParsed's `explicitCmdLine`:

https://github.com/alex-torok/reproduce_bazel_explicit_cmd_line/blob/059edadb147b229a97dd8c410d8e50971e21ed05/optionsParsedMsg_customFlag.json#L1-L30

---


```
bazel --nohome_rc build --//:alias_value=foo --build_event_json_file=bes.json ...; jq 'select(has("optionsParsed"))' bes.json > optionsParsedMsg_customFlag.json
```

I would expect to see `--//:alias_value=foo` inside of the optionsParsed's `explicitCmdLine`:

https://github.com/alex-torok/reproduce_bazel_explicit_cmd_line/blob/059edadb147b229a97dd8c410d8e50971e21ed05/optionsParsedMsg_customFlag.json#L1-L30
