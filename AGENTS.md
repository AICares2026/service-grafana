## Stack
Grafana dashboard-as-code repository. JSON (Grafana dashboard definitions), YAML (provisioning configuration). No application runtime language detected.

## Constraints
Never modify:
- `*.lock` files of any kind
- Any file containing credentials, secrets, or API keys (check for `password`, `apiKey`, `secret` patterns)
- `provisioning/notifiers/` — alerting credential configs
- `provisioning/datasources/` — may contain embedded credentials
- Auto-generated or vendor directories if present

## Conventions
- Grafana dashboard JSON files live under `dashboards/` (or subdirectories); filenames end in `.json`
- Provisioning config files live under `provisioning/` and end in `.yaml` or `.yml`
- Dashboard JSON must pass `dashboard_json_lint` — validate `__inputs__`, `__requires__`, `panels`, and `schemaVersion` fields are present and well-formed
- YAML provisioning files must be valid YAML with correct Grafana provisioning schema (`apiVersion`, `providers` or `datasources` top-level keys)
- One dashboard per `.json` file; do not merge dashboards

## Dependency manifests
- Any `.yaml`/`.yml` files under `provisioning/` that pin a Grafana version or image tag
- Check repository root for `docker-compose.yml` or `Dockerfile` — these may pin the Grafana image version (e.g. `grafana/grafana:10.x.x`)
- No `requirements.txt`, `go.mod`, or `package.json` expected; if found, do not modify without explicit instruction
