# System Patterns

- **Typed schemas** defined in `src/types.ts` using Zod provide validation and TypeScript types.
- **Protocol** logic in `src/shared/protocol.ts` coordinates requests, responses, and notifications over a pluggable `Transport` interface.
- **Server** implementation in `src/server/` extends `Protocol` and handles initialization, capability negotiation, and OAuth flows. `src/server/mcp.ts` offers high-level APIs for registering tools, resources, and prompts.
- **Client** implementation in `src/client/` mirrors the server and supports multiple transports.
- **Transports** (stdio, Streamable HTTP, SSE, WebSocket) live under `src/server/` and `src/client/` folders.
- Builds produce ESM and CJS output under `dist/` using separate TypeScript configs.
