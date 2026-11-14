# github-core-clone-01 — Deterministic Single-File Git Forge (`icolumbina`)

A zero-dependency GitHub-compatible forge built in `app.ts` and `main.ts` (`createApp`) using only Node 22 standard library primitives (`node:http`, `node:crypto`, `node:zlib`).

## Core Capabilities & Optimizations

1. **Smart HTTP Git Transport (`upload-pack`, `receive-pack`, `packfile`)**:
   - Implements Git wire protocol v2 `upload-pack` (`ls-refs`, `fetch`, `shallow`, `ofs-delta`) and v0 `receive-pack` (`report-status`, `side-band-64k`, `delete-refs`) with deterministic SHA-1 `packfile` generation.
   - Reuses pre-deflated object chunks (`packEntry`) and memoizes reachable tree closures (`treeClosureCache`) to minimize latency on repeated clones and fetches.
2. **Object & Tree WeakMap Caches (`icTreeWeakCache`, `icCommitWeakCache`, `icTagWeakCache`)**:
   - Eliminates redundant buffer decoding across commit ancestry walks, three-way merge base resolution, and `flatTreeCache` tree diffing.
3. **REST v3 (`issues`, `pulls`, `refs`), `graphql` v4, and `mcp` Endpoints**:
   - Full `/api/v3` coverage for repositories, `refs`, branches, commits, contents, labels, `issues`, and `pulls`.
   - Query-memoized `graphql` v4 execution (`icGqlDocumentCache`) and streamable HTTP `mcp` tool server (`POST /mcp`).
