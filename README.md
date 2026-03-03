# Local AI Knowledge Base (Qwen 7B + Embedding + Reranker)

这是一个从零实现的本地 RAG 知识库系统：

- 上传 `Markdown / PDF / TXT`
- 本地分块与索引
- 本地 embedding：`Xenova/bge-m3`
- 本地 reranker：`onnx-community/bge-reranker-v2-m3-ONNX`
- 本地生成模型：`qwen2.5:7b-instruct`（通过 Ollama 运行）
- 返回答案时附带引用来源（文件名、页码/段号、chunk）

## 项目路径

```text
e:\vscode\local-ai-knowledge-base
```

## 模型下载位置

1. LLM（Qwen 7B）
- 下载方式：`ollama pull qwen2.5:7b-instruct`
- 模型页面：https://ollama.com/library/qwen2.5

2. Embedding 模型
- 模型名：`Xenova/bge-m3`
- 页面：https://huggingface.co/Xenova/bge-m3
- 下载方式：后端首次运行或 `npm run warmup` 自动下载到本机缓存

3. Reranker 模型
- 模型名：`onnx-community/bge-reranker-v2-m3-ONNX`
- 页面：https://huggingface.co/onnx-community/bge-reranker-v2-m3-ONNX
- 下载方式：后端首次运行或 `npm run warmup` 自动下载到本机缓存

## 快速启动

详细步骤见 [SETUP.md](./SETUP.md)。

核心顺序：

1. 启动 Chroma
2. 启动 Ollama 并拉取 qwen2.5:7b-instruct
3. 启动后端（可先 warmup）
4. 启动前端

## API

- `GET /api/health`
- `GET /api/files`
- `POST /api/upload`
- `POST /api/chat`
