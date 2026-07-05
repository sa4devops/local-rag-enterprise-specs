# OSS_REFERENCE_CATALOG.md — Approved Open-Source Reference Catalog

> This file lists open-source projects that AI Coding Agents may study as references under the Reference-aware clean implementation policy.
>
> These projects are references, not dependencies.
> Do not copy code directly unless license review explicitly approves it.

## Rules

AI Coding Agents may:

- read the linked repositories
- study architecture
- study UI flows
- study API patterns
- study folder structures
- study integration approaches
- write notes and comparisons
- implement original code that fits this project

AI Coding Agents must not:

- copy full files
- copy long snippets
- rename copied code and treat it as original
- remove attribution or notices
- introduce dependencies without license review
- introduce AGPL/SSPL/copyleft code without explicit approval

## Reference Catalog

| ID | Project | URL | Category | Why we study it | Allowed learning | Not allowed | License status | Phase |
|---|---|---|---|---|---|---|---|---|
| REF-001 | Open WebUI | https://github.com/open-webui/open-webui | UX / AI UI / RAG | Study local AI UI, model management, RAG flows, admin experience | UX patterns, feature behavior, provider concepts | Do not copy code/files; do not make it final UI | Needs license review before any direct reuse | Phase 1+ |
| REF-002 | Continue | https://github.com/continuedev/continue | AI coding assistant | Study agent/developer workflow and context handling | Agent UX, workspace context, prompt flows | Do not copy implementation | Needs review | Future |
| REF-003 | Dify | https://github.com/langgenius/dify | Workflow / LLM apps | Study app builder, workflows, model providers | Workflow UX, app concepts, provider design | Do not copy backend/frontend | Needs review | Phase 3+ |
| REF-004 | Flowise | https://github.com/FlowiseAI/Flowise | Visual AI workflows | Study node-based workflow builder | Node/canvas UX, workflow concepts | Do not copy nodes/code | Needs review | Phase 3+ |
| REF-005 | Appsmith | https://github.com/appsmithorg/appsmith | Internal tools / screen builder | Study enterprise screen builder and data binding | Screen builder UX, datasource binding concepts | Do not copy code | Needs review | Phase 1+ |
| REF-006 | Budibase | https://github.com/Budibase/budibase | Internal apps / forms | Study low-code forms, tables, workflows | Forms/tables UX, app builder concepts | Do not copy code | Needs review | Phase 1+ |
| REF-007 | NocoDB | https://github.com/nocodb/nocodb | Data UI / tables | Study database table UI and permissions | Table UX, schema-driven views | Do not copy code | Needs review | Phase 2+ |
| REF-008 | Directus | https://github.com/directus/directus | Data platform / admin | Study metadata-driven admin/data platform | Admin UX, permissions, collections | Do not copy code | Needs review | Phase 2+ |
| REF-009 | Langfuse | https://github.com/langfuse/langfuse | LLM observability | Study LLM traces and prompt/session observability | Observability concepts only | Do not add as dependency without review | Needs review | Future |
| REF-010 | Haystack | https://github.com/deepset-ai/haystack | RAG pipelines | Study RAG pipeline architecture | Pipeline concepts, retrieval patterns | Do not copy code | Needs review | Phase 4+ |
| REF-011 | LlamaIndex | https://github.com/run-llama/llama_index | RAG / indexing | Study indexing and document workflows | Architecture and patterns | Direct dependency requires review | Needs review | Phase 4+ |
| REF-012 | Unstructured | https://github.com/Unstructured-IO/unstructured | Document parsing | Study document ingestion/parsing | Parsing concepts and file processing | Direct dependency requires review | Needs review | Phase 5 |
