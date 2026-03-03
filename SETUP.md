# SETUP

以下是 Windows 环境下的完整启动流程。

## 1) 进入新项目目录

```powershell
cd e:\vscode\local-ai-knowledge-base
Copy-Item .env.example .env
```

## 2) 准备依赖

### 2.1 安装并启动 Chroma

```powershell
docker compose up -d
docker compose ps
```

预期：`http://localhost:8000` 可用。

### 2.2 安装 Ollama 并下载 Qwen 7B

1. 安装地址：https://ollama.com/download/windows
2. 拉取模型：

```powershell
ollama pull qwen2.5:7b-instruct
```

3. 可选验证：

```powershell
ollama run qwen2.5:7b-instruct "你好"
```

## 3) 启动后端

```powershell
cd e:\vscode\local-ai-knowledge-base\backend
npm install
npm run warmup
npm run dev
```

说明：
- `npm run warmup` 会预下载并预热 embedding/reranker 模型。
- 首次下载可能较慢，后续启动会快很多。

## 4) 启动前端

新开一个终端：

```powershell
cd e:\vscode\local-ai-knowledge-base\frontend
npm install
npm run dev
```

前端地址：`http://localhost:5173`

## 5) 验证

### 5.1 健康检查

```powershell
curl.exe http://localhost:3001/api/health
```

### 5.2 上传文档

```powershell
curl.exe -X POST "http://localhost:3001/api/upload" `
  -F "file=@e:\vscode\local-ai-knowledge-base\sample.md"
```

### 5.3 提问

```powershell
curl.exe -X POST "http://localhost:3001/api/chat" `
  -H "Content-Type: application/json" `
  -d "{\"question\":\"请总结文档重点\",\"topK\":5,\"retrievalCandidateK\":12}"
```

## 6) 模型下载来源

1. Qwen 7B（Ollama）
- https://ollama.com/library/qwen2.5

2. Embedding
- https://huggingface.co/Xenova/bge-m3

3. Reranker
- https://huggingface.co/onnx-community/bge-reranker-v2-m3-ONNX

## 常见问题

1. `Ollama request failed`
- 检查 Ollama 是否运行，`OLLAMA_BASE_URL` 是否正确（默认 `http://127.0.0.1:11434`）。

2. 首次提问很慢
- 正常，embedding/reranker 首次会下载模型。

3. `知识库中未找到可用依据。`
- 表示当前检索未命中可靠片段，请补充文档或优化提问。
