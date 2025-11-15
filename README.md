# word-hero-api

## API Documentation

The canonical REST contract is defined as OpenAPI in [`docs/openapi.yaml`](docs/openapi.yaml).

### Refresh Workflow
1. Clone the upstream implementation into the scratch space mandated by `agent_read.md`:
   ```bash
   mkdir -p .tmp/repos
   git clone https://github.com/sanmu2018/word-hero .tmp/repos/word-hero
   ```
2. Diff `.tmp/repos/word-hero/internal/router` and `internal/dto` to capture handler or schema changes. Update `docs/openapi.yaml` accordingly and bump the commit hash recorded in the spec description.
3. Reference the updated spec (or a rendered artifact) from your pull request so downstream services know a new API revision is available.
