# 微服务业务规范
```text
首先遵从agent_read_v2.md
```
# Repository Guidelines

Read `agent_read.md` first; this guide captures the rules to remember afterward.

## Project Structure & Module Organization
The root holds coordination files (`agent_read.md`, `agent_service.yaml`, `README.md`, `LICENSE`) and should expand around a `src/` tree for this API service. Keep controllers inside `src/modules/<feature>`, shared helpers in `src/lib/`, and DTOs or schema definitions under `src/contracts/` so runtime code and tests read the same types. Mirror feature folders under `tests/unit` or `tests/integration`, store fixtures in `tests/fixtures/`, and park OpenAPI specs inside `docs/api/` to match the role from `agent_service.yaml`.

## Build, Test, and Development Commands
- `npm install` – install dependencies once `package.json` exists; use Node 20 LTS.
- `npm run dev` – run the API in watch mode (nodemon or ts-node-dev) while iterating locally.
- `npm run build` – emit production assets to `dist/` and stop on type errors.
- `npm test` – run the Jest/Vitest suite; add `--watch` for fast loops or `--runInBand` for debugging.

## Coding Style & Naming Conventions
Use TypeScript targeting ES2022, 2-space indentation, trailing commas, and single quotes enforced through `npm run lint` (ESLint + Prettier). Name files in kebab-case (`word-set.controller.ts`), classes or types in PascalCase, functions in camelCase, and environment variables in SCREAMING_SNAKE_CASE. Store request/response contracts in `*.dto.ts` files and suffix interfaces with `Props` or `Payload` for clarity.

## Testing Guidelines
Use Jest or Vitest with Supertest support, keeping fast logic specs in `tests/unit` and slower HTTP or database checks in `tests/integration`. Name spec files `<feature>.spec.ts`, stub upstream systems with fixtures, and require `npm test -- --coverage` to remain at or above 85% statements. Execute the suite once with `NODE_ENV=test` and once with `NODE_ENV=ci` before opening a PR.

## Commit & Pull Request Guidelines
Adopt Conventional Commits (`feat: add puzzle scoring endpoint`, `fix: guard empty clues`) so automation can parse the log. Reference the driving issue in the footer (`Refs #42`), summarize intent, implementation notes, and test evidence in the PR body, and attach cURL transcripts or screenshots whenever responses change. Link the agent-issued task and highlight any config or data migrations reviewers must run.

## Security & Configuration Tips
Load secrets from `.env.local`, document required keys in `.env.example`, and keep both files out of version control. Update `agent_service.yaml` whenever this service’s role or dependencies change so orchestration remains accurate, and validate each endpoint against the OpenAPI spec in `docs/api/`. Inspect other services only through the disposable `.tmp/repos/` workspace.
