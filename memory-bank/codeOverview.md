# Code Overview

This file catalogues the purpose of the main directories and notable files in the repository. Use it as a map when exploring or modifying the codebase.

## Root Files
- `package.json` – npm metadata, scripts (`build`, `lint`, `test`) and dependency list.
- `tsconfig.json` – primary TypeScript configuration targeting ESM output under `dist/esm`.
- `tsconfig.cjs.json` – secondary config extending the base config to emit CommonJS modules in `dist/cjs`.
- `tsconfig.prod.json` – stripped down config used when publishing.

## `src/` Directory
Contains all TypeScript source files.

### Common Definitions
- `src/types.ts` – all Zod schemas for MCP messages. Inferred types are exported for external use.
- `src/shared/` – protocol primitives and utilities:
  - `protocol.ts` – core `Protocol` class for JSON‑RPC over a `Transport`.
  - `transport.ts` – defines the `Transport` interface used by client and server implementations.
  - `auth.ts`, `stdio.ts`, `uriTemplate.ts` – helpers shared between client and server.

### Server Side
- `src/server/index.ts` – `Server` class extending `Protocol`; handles initialization and capability negotiation.
- `src/server/mcp.ts` – higher‑level `McpServer` exposing APIs to register tools, resources and prompts.
- `src/server/stdio.ts`, `sse.ts`, `streamableHttp.ts` – server‑side transports.
- `src/server/auth/` – OAuth implementation (routers, providers, middleware).
- `src/server/completable.ts` – helper for streaming completion responses.

### Client Side
- `src/client/index.ts` – `Client` class used by consumers to connect to an MCP server.
- `src/client/stdio.ts`, `sse.ts`, `streamableHttp.ts`, `websocket.ts` – client transports.
- `src/client/auth.ts` – OAuth helper for obtaining tokens.

### Utilities and Tests
- `src/cli.ts` – minimal CLI for launching example servers or clients.
- `src/examples/` – demonstration projects showing usage patterns.
- `src/__mocks__/` – Jest mocks used in unit tests.
- `*.test.ts` files – unit test suites for the corresponding modules.

## Build Output
Running `npm run build` compiles the above sources into `dist/`:
- `dist/esm/` – ES modules with `package.json` specifying `"type": "module"`.
- `dist/cjs/` – CommonJS build generated via `tsconfig.cjs.json`.

Only the contents of `dist/` are published to npm.
