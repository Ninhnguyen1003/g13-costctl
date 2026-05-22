# Reflections — G13 costctl

1. Multi-account: To run `costctl` across many accounts I would implement an account loop that assumes a cross-account role in each target account (using `sts:AssumeRole`) and builds a boto3 session per account. The CLI would accept an `--accounts` list or read from a config file. Outputs would be emitted per-account (CSV or JSON) and aggregated centrally; errors and throttling would be captured and retried with backoff.

2. Clean blast radius & safety: For `clean --apply` I would add an approval step showing counts and requiring a typed confirmation (e.g. type the tag value), restrict by allowed namespaces (only run in personal sandbox accounts), and add a `--max` cap to limit number of deletions. I would also implement a dry-run audit log and an `undo` plan when possible (snapshots for volumes before deletion).

(You can edit these answers before final submission.)
