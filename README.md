# OpenAI Developer Documentation

<p align="center"><a href="README.md"><b>English</b></a> | <a href="README_cn.md">中文</a></p>

Last Update:2026-08-03 18:00:00

This is a local knowledge base organized from the official OpenAI developer documentation. It is used to look up API endpoints, request parameters, response structures, code examples, streaming events, Realtime events, development guides, and related developer product materials.

Each document retains the official `source_url`. When encountering version differences, field limitations, or uncertainty about parsing results, verify against the official source.

## Getting Started

Start with `index.json`. It is the directory entry of this knowledge base, providing:

- `document_count`: number of organized document entries.
- `categories`: category names and entry counts per category.
- `files`: corresponding category JSON files.

Category JSON files are located at the root of this directory, e.g. `responses.json`, `chat.json`, `files.json`. Each file contains the complete document entries for one category.

## Contents

### API Endpoints

The following categories primarily document REST API endpoints. Each entry typically includes the HTTP method, URI, request type, path parameters, query parameters, request body fields, response fields, and request/response examples:

- `responses.json`: Responses API, model responses, input items, token statistics, cancellation, and compression.
- `chat.json`: Chat Completions API.
- `completions.json`: Legacy Completions API.
- `audio.json`: Speech generation, transcription, translation, voices, and voice licensing.
- `images.json`: Image generation, editing, and variations.
- `videos.json`: Video creation, querying, deletion, editing, extension, and downloading.
- `files.json`, `uploads.json`: File upload, file management, and chunked uploads.
- `containers.json`: Containers and container files.
- `vector_stores.json`: Vector stores, search, files, and file batches.
- `models.json`: Model queries, listing, and deletion.
- `embeddings.json`: Text embeddings.
- `moderations.json`: Content moderation.
- `content_provenance_checks.json`: Content provenance checks.

### Complex Capabilities and Task-Oriented APIs

- `evals.json`: Evaluations, evaluation runs, and output items.
- `fine_tuning.json`: Fine-tuning jobs, checkpoints, permissions, and Grader.
- `realtime.json`: Realtime sessions, calls, client secrets, and SIP/telephony capabilities.
- `admin.json`: Organizations, projects, users, roles, service accounts, certificates, audit logs, quotas, and usage.
- `beta.json`: Beta APIs, including Assistants, Threads, Runs, ChatKit, and Beta Responses related interfaces.
- `skills.json`: Skills and skill versions.

### Guides and Overviews

- `api_guides.json`: Guides for Agents, Tools, Realtime, and production practices.
- `api_docs.json`: API documentation entry points, model descriptions, and related docs.
- `reference_overviews.json`: API Reference overviews, Responses/Chat/Realtime overviews, event documentation, and other reference pages.
- `other.json`: Codex, ChatGPT, plugins, Workspace Agents, Commerce, Ads, Learn, Showcase, Blog, Cookbook, and Community pages.

## Finding by Topic

### "I want to call an API"

1. Choose a category based on the capability, e.g., `responses.json` for model responses, `files.json` for file uploads, `images.json` for image generation.
2. Search within `documents` by `title`, `endpoint.method`, or `endpoint.uri`.
3. Read the `endpoint`, relevant parameters, `request_body_schema`, and request examples.
4. For return values, further read `response_schema` and response examples.

### "How do I fill in this parameter?"

1. First locate the document entry by endpoint.
2. Find the parameter in `parameters.path`, `parameters.query`, or `parameters.body`.
3. Read the parameter's `type`, `optional`, `nullable`, `description`, and `children`.
4. `children` represent nested objects or array elements — you must recurse into them.
5. If the description includes model constraints, default values, enum values, or deprecation notes, do not only check the type — read the description as well.

### "What do the request and response look like?"

- Request structure: see `request_body_schema` and entries in `examples` with `purpose` set to `request`.
- Response structure: see `response_schema` and entries in `examples` with `purpose` set to `response`.
- Full HTTP call: typically look at examples with `language` set to `http` or `bash`.
- SDK calls: check for `python`, `javascript`, or other language code blocks in examples; if absent, generate based on the API structure.

### "I want to use streaming or Realtime"

1. First look at the corresponding create/connect endpoint in `responses.json`, `chat.json`, or `realtime.json`.
2. Then look at the streaming events or client/server event documentation in `reference_overviews.json`.
3. Event documents may not have a REST `endpoint` — do not treat event names as URIs.
4. Read the event entry's `events_or_schemas` and `examples` to confirm the event direction, event type, and field structure.

### "I want to set up production deployment or organization management"

- Authentication, request IDs, errors, rate limits, and production advice: see `api_guides.json`.
- Organizations, projects, users, roles, service accounts, and usage: see `admin.json`.
- Model capabilities and model selection: see `models.json`, `api_docs.json`, and related guides.

## How to Read JSON Entries

The structure of a category file is:

```json
{
  "category": "responses",
  "count": 1,
  "documents": []
}
```

- `category`: the current category.
- `count`: the number of entries.
- `documents`: array of document entries.

The main fields for a single API entry are:

```json
{
  "title": "Create a model response",
  "source_url": "https://developers.openai.com/api/reference/...",
  "endpoint": {
    "method": "POST",
    "uri": "/responses",
    "request_type": "application/json"
  },
  "description": "...",
  "parameters": {
    "path": [],
    "query": [],
    "body": []
  },
  "request_body_schema": [],
  "response_schema": [],
  "examples": [],
  "events_or_schemas": []
}
```

### Basic Fields

- `title`: the official page title.
- `source_url`: the official source URL, also the final reference for verification.
- `description`: the purpose and main description of the endpoint.

### `endpoint`

- `method`: HTTP method, e.g., `GET`, `POST`, `PATCH`, `DELETE`.
- `uri`: API path, e.g., `/responses`, `/files/{file_id}`. Typically needs to be prefixed with `https://api.openai.com/v1`.
- `request_type`: request content type. JSON endpoints are usually `application/json`, file uploads are usually `multipart/form-data`.

Overview pages, event pages, and schema pages may set these values to `null`. This indicates the page is not a regular REST endpoint — do not infer a method or URI.

### Parameter Fields

Parameters are organized under `parameters` by source location:

- `path`: path variables in the URI.
- `query`: URL query parameters.
- `body`: JSON request body fields.
- Other names: retain special parameter groupings from the official documentation.

Each parameter includes:

- `name`: field name.
- `type`: official type description, may be a union type or enum.
- `optional`: whether it can be omitted.
- `nullable`: whether an explicit `null` is allowed. This is not equivalent to `optional`.
- `description`: purpose, constraints, default behavior, enums, and deprecation info.
- `children`: nested fields — must be inspected recursively when reading object structures.

### Schema and Example Fields

- `request_body_schema`: a convenient index of request body fields.
- `response_schema`: successful response fields and their nested structure.
- `examples`: code or data examples. Each entry contains `language`, `purpose`, `context`, and `code`.
- `events_or_schemas`: streaming events, Realtime events, or schema section names.

Model IDs, object IDs, timestamps, file paths, and `VAR_` placeholders in examples should not be treated as fixed business values. API Keys must only be provided through environment variables or secret management services.

## Accuracy Rules

- This knowledge base is a snapshot of the documentation at the time of capture and does not automatically represent the current live version.
- The official page corresponding to `source_url` is the final source of truth for verification.
- `Deprecated` fields may appear in the documentation, but new code should prefer the officially recommended replacement fields.
- Beta or legacy endpoints should be clearly marked with their version status and not conflated with stable endpoints.
- Do not guess request structure from field names; prefer the schema, field descriptions, and official examples.
- Do not put response fields in the request body, nor query parameters in the JSON body.
- Do not fill in fields, methods, URIs, defaults, or compatibility that the documentation does not explicitly specify.
