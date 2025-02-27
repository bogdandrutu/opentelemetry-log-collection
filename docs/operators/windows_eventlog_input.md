## `windows_eventlog_input` operator

The `windows_eventlog_input` operator reads logs from the windows event log API.

### Configuration Fields

| Field           | Default                  | Description                                                                                                                    |
| ---             | ---                      | ---                                                                                                                            |
| `id`            | `windows_eventlog_input` | A unique identifier for the operator                                                                                           |
| `output`        | Next in pipeline         | The connected operator(s) that will receive all outbound entries                                                               |
| `channel`       | required                 | The windows event log channel to monitor                                                                                       |
| `max_reads`     | 100                      | The maximum number of bodies read into memory, before beginning a new batch                                                   |
| `start_at`      | `end`                    | On first startup, where to start reading logs from the API. Options are `beginning` or `end`                                   |
| `poll_interval` | 1s                       | The interval at which the channel is checked for new log entries. This check begins again after all new bodies have been read |
| `write_to`      | $                        | The body [field](/docs/types/field.md) written to when creating a new log entry                                              |
| `attributes`    | {}                       | A map of `key: value` pairs to add to the entry's attributes                                                                      |
| `resource`      | {}                       | A map of `key: value` pairs to add to the entry's resource                                                                    |

### Example Configurations

#### Simple

Configuration:
```yaml
- type: windows_eventlog_input
  channel: application
```

Output entry sample:
```json
{
  "timestamp": "2020-04-30T12:10:17.656726-04:00",
  "severity": 30,
  "body": {
		"event_id": {
			"qualifiers": 0,
			"id": 1000
		},
		"provider": {
			"name": "provider name",
			"guid": "provider guid",
			"event_source": "event source"
		},
		"system_time": "2020-04-30T12:10:17.656726789Z",
		"computer": "example computer",
		"channel": "application",
		"record_id": 1,
		"level": "Information",
		"message": "example message",
		"task": "example task",
		"opcode": "example opcode",
		"keywords": ["example keyword"]
	}
}
```
