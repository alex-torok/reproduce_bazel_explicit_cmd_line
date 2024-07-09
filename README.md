# Showcase aliases and custom flags not appearing in explicit_cmd_line field

```
bazel --nohome_rc build --alias=foo --build_event_json_file=bes.json ...; jq 'select(has("optionsParsed"))' bes.json > optionsParsedMsg_alias.json
```

I would expect to see `--alias=foo` inside of the optionsParsed's `explicitCmdLine`:

**optionsParsedMsg_alias.json**:

```json
{
  "id": {
    "optionsParsed": {}
  },
  "optionsParsed": {
    "startupOptions": [
      "--max_idle_secs=10800",
      "--noshutdown_on_low_sys_mem",
      "--connect_timeout_secs=30",
      "--output_user_root=/ephemeral/bazel",
      "--output_base=/ephemeral/bazel/66a32df71783bd2efd1b3a8e49820a60",
      "--failure_detail_out=/ephemeral/bazel/66a32df71783bd2efd1b3a8e49820a60/failure_detail.rawproto",
      "--expand_configs_in_place",
      "--idle_server_tasks",
      "--write_command_log",
      "--nowatchfs",
      "--nofatal_event_bus_exceptions",
      "--nowindows_enable_symlinks",
      "--noclient_debug"
    ],
    "explicitStartupOptions": [
      "--output_user_root=/ephemeral/bazel"
    ],
    "cmdLine": [
      "--flag_alias=alias=//:alias_value",
      "--build_event_json_file=bes.json"
    ],
    "explicitCmdLine": [
      "--build_event_json_file=bes.json"
    ],
    "invocationPolicy": {}
  }
}
```

---


```
bazel --nohome_rc build --//:alias_value=foo --build_event_json_file=bes.json ...; jq 'select(has("optionsParsed"))' bes.json > optionsParsedMsg_customFlag.json
```

I would expect to see `--//:alias_value=foo` inside of the optionsParsed's `explicitCmdLine`:

**optionsParsedMsg_customFlag.json**:
```json
{
  "id": {
    "optionsParsed": {}
  },
  "optionsParsed": {
    "startupOptions": [
      "--max_idle_secs=10800",
      "--noshutdown_on_low_sys_mem",
      "--connect_timeout_secs=30",
      "--output_user_root=/ephemeral/bazel",
      "--output_base=/ephemeral/bazel/66a32df71783bd2efd1b3a8e49820a60",
      "--failure_detail_out=/ephemeral/bazel/66a32df71783bd2efd1b3a8e49820a60/failure_detail.rawproto",
      "--expand_configs_in_place",
      "--idle_server_tasks",
      "--write_command_log",
      "--nowatchfs",
      "--nofatal_event_bus_exceptions",
      "--nowindows_enable_symlinks",
      "--noclient_debug"
    ],
    "explicitStartupOptions": [
      "--output_user_root=/ephemeral/bazel"
    ],
    "cmdLine": [
      "--flag_alias=alias=//:alias_value",
      "--build_event_json_file=bes.json"
    ],
    "explicitCmdLine": [
      "--build_event_json_file=bes.json"
    ],
    "invocationPolicy": {}
  }
}
```
