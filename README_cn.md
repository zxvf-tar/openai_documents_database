# OpenAI Developer Documentation

<p align="center"><a href="README.md">English</a> | <a href="README_cn.md"><b>中文</b></a></p>

Last Update:2026-08-03 18:00:00

这是一个按 OpenAI 官方开发者文档整理的本地知识库。它用于查找 API 接口、请求参数、响应结构、代码示例、流式事件、Realtime 事件、开发指南以及相关开发者产品资料。

每条文档都保留了官方 `source_url`，遇到版本差异、字段限制或解析结果不确定时，应回到官方来源核对。

## 从哪里开始

先看 `index.json`。它是本知识库的目录入口，提供：

- `document_count`：已整理的文档条目数量。
- `categories`：分类名称及每类条目数量。
- `files`：对应的分类 JSON 文件。

分类 JSON 文件位于本目录根部，例如 `responses.json`、`chat.json`、`files.json`。每个文件包含一个分类下的完整文档条目。

## 有什么内容

### API 接口

以下分类主要记录 REST API 接口，每条记录通常包含 HTTP 方法、URI、请求类型、路径参数、查询参数、请求体字段、响应字段和请求/响应示例：

- `responses.json`：Responses API，模型响应、输入项、令牌统计、取消和压缩。
- `chat.json`：Chat Completions API。
- `completions.json`：旧版 Completions API。
- `audio.json`：语音生成、转录、翻译、声音和语音许可。
- `images.json`：图像生成、编辑和变体。
- `videos.json`：视频创建、查询、删除、编辑、扩展和下载。
- `files.json`、`uploads.json`：文件上传、文件管理和分块上传。
- `containers.json`：容器及容器文件。
- `vector_stores.json`：向量存储、搜索、文件和文件批处理。
- `models.json`：模型查询、列表和删除。
- `embeddings.json`：文本嵌入。
- `moderations.json`：内容审核。
- `content_provenance_checks.json`：内容来源检查。

### 复杂能力和任务型 API

- `evals.json`：评测、评测运行和输出项。
- `fine_tuning.json`：微调任务、检查点、权限和 Grader。
- `realtime.json`：Realtime 会话、调用、客户端密钥和 SIP/电话相关能力。
- `admin.json`：组织、项目、用户、角色、服务账号、证书、审计日志、配额和用量。
- `beta.json`：Beta API，包括 Assistants、Threads、Runs、ChatKit 和 Beta Responses 相关接口。
- `skills.json`：技能及技能版本。

### 指南和概览

- `api_guides.json`：Agents、Tools、Realtime 和生产实践指南。
- `api_docs.json`：API 文档入口、模型说明等文档。
- `reference_overviews.json`：API Reference 总览、Responses/Chat/Realtime 概览、事件文档和其他参考页。
- `other.json`：Codex、ChatGPT、插件、Workspace Agents、Commerce、Ads、Learn、Showcase、Blog、Cookbook 和 Community 等页面。

## 按问题查找

### “我想调用某个接口”

1. 根据能力选择分类，例如生成模型回复看 `responses.json`，上传文件看 `files.json`，生成图片看 `images.json`。
2. 在 `documents` 中按 `title`、`endpoint.method` 和 `endpoint.uri` 查找。
3. 读取 `endpoint`、相关参数、`request_body_schema` 和请求示例。
4. 需要返回值时继续读取 `response_schema` 和响应示例。

### “这个参数怎么填”

1. 先根据接口定位文档条目。
2. 在 `parameters.path`、`parameters.query` 或 `parameters.body` 中查找参数。
3. 读取参数的 `type`、`optional`、`nullable`、`description` 和 `children`。
4. `children` 表示嵌套对象或数组元素，必须继续递归查看。
5. 如果描述包含模型限制、默认值、枚举值或弃用说明，不要只看类型，必须同时阅读描述。

### “请求和响应长什么样”

- 请求结构：看 `request_body_schema` 和 `examples` 中 `purpose` 为 `request` 的条目。
- 响应结构：看 `response_schema` 和 `examples` 中 `purpose` 为 `response` 的条目。
- 完整 HTTP 调用：通常看 `language` 为 `http` 或 `bash` 的示例。
- SDK 调用：查看示例中的 `python`、`javascript` 或其他语言代码块；若没有，则根据接口结构生成。

### “我要使用流式或 Realtime”

1. 先看 `responses.json`、`chat.json` 或 `realtime.json` 中对应的创建/连接接口。
2. 再看 `reference_overviews.json` 中的流式事件或客户端/服务器事件文档。
3. 事件文档可能没有 REST `endpoint`，不要把事件名称当成 URI。
4. 读取事件条目的 `events_or_schemas` 和 `examples`，确认事件方向、事件类型和字段结构。

### “我要做生产部署或组织管理”

- 认证、请求 ID、错误、限流和生产建议：看 `api_guides.json`。
- 组织、项目、用户、角色、服务账号和用量：看 `admin.json`。
- 模型能力和模型选择：看 `models.json`、`api_docs.json` 以及相关指南。

## JSON 条目怎么看

分类文件的结构是：

```json
{
 "category": "responses",
 "count": 1,
 "documents": []
}
```

- `category`：当前分类。
- `count`：条目数量。
- `documents`：文档条目数组。

单个接口条目的主要字段如下：

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

### 基本字段

- `title`：官方页面标题。
- `source_url`：官方来源地址，也是最终核对入口。
- `description`：接口用途和主要说明。

### `endpoint`

- `method`：HTTP 方法，例如 `GET`、`POST`、`PATCH`、`DELETE`。
- `uri`：API 路径，例如 `/responses`、`/files/{file_id}`。通常需要与 `https://api.openai.com/v1` 拼接。
- `request_type`：请求内容类型。JSON 接口通常是 `application/json`，文件上传通常是 `multipart/form-data`。

概览页、事件页和 Schema 页可能将这些值设为 `null`。这表示页面不是普通 REST 接口，不能自行补写方法或 URI。

### 参数字段

参数按来源位置放在 `parameters` 下：

- `path`：URI 中的路径变量。
- `query`：URL 查询参数。
- `body`：JSON 请求体字段。
- 其他名称：保留官方文档中的特殊参数分组。

每个参数包含：

- `name`：字段名。
- `type`：官方类型描述，可能是联合类型或枚举。
- `optional`：是否可以省略。
- `nullable`：是否允许显式使用 `null`。它和 `optional` 不等价。
- `description`：用途、限制、默认行为、枚举和弃用信息。
- `children`：嵌套字段，读取对象结构时必须递归查看。

### Schema 和示例字段

- `request_body_schema`：请求体字段的便捷索引。
- `response_schema`：成功响应字段及其嵌套结构。
- `examples`：代码或数据示例。每项包含 `language`、`purpose`、`context` 和 `code`。
- `events_or_schemas`：流式事件、Realtime 事件或 Schema 章节名称。

示例中的模型 ID、对象 ID、时间戳、文件路径和 `VAR_` 占位符都不应直接当作固定业务值。API Key 只能通过环境变量或密钥管理服务提供。

## 使用时的准确性规则

- 本知识库是抓取时的文档快照，不自动代表当前线上版本。
- 以 `source_url` 对应的官方页面为最终核对来源。
- `Deprecated` 字段可以在文档中出现，但新代码应优先使用官方推荐的替代字段。
- Beta 或旧版接口应明确标注其版本属性，不要与正式接口混为一谈。
- 不要根据字段名称猜测请求结构；优先使用 Schema、字段描述和官方示例。
- 不要把返回字段放入请求体，也不要把查询参数放进 JSON body。
- 不要为文档没有明确说明的字段、方法、URI、默认值或兼容性自行补值。
