# Python API, HTTP Backend & MCP Server

Reference compiled from [PDFMathTranslate `docs/APIS.md`](https://github.com/PDFMathTranslate/PDFMathTranslate/blob/main/docs/APIS.md), `docs/ADVANCED.md`, and `pdf2zh/mcp_server.py`.

## 1. Python API

`pdf2zh` exposes `translate` and `translate_stream`:

```python
from pdf2zh import translate, translate_stream

params = {
    "lang_in": "en",
    "lang_out": "zh",
    "service": "google",
    "thread": 4,
}

# Translate local file(s)
(file_mono, file_dual) = translate(files=["example.pdf"], **params)[0]

# Translate in-memory bytes stream
with open("example.pdf", "rb") as f:
    (stream_mono, stream_dual) = translate_stream(stream=f.read(), **params)
```

## 2. HTTP Backend API

Requires Redis plus `pip install 'pdf2zh[backend]'`:

```bash
# Start Flask API (port 11008) and Celery worker
pdf2zh --flask
pdf2zh --celery worker
```

Submit and retrieve tasks over HTTP:

```bash
# Submit translation task
curl http://localhost:11008/v1/translate \
  -F "file=@example.pdf" \
  -F 'data={"lang_in":"en","lang_out":"zh","service":"google","thread":4}'
# Returns: {"id":"<task_id>"}

# Poll task progress / status
curl http://localhost:11008/v1/translate/<task_id>

# Download monolingual / bilingual outputs once state == "SUCCESS"
curl http://localhost:11008/v1/translate/<task_id>/mono --output example-mono.pdf
curl http://localhost:11008/v1/translate/<task_id>/dual --output example-dual.pdf

# Cancel and delete task
curl -X DELETE http://localhost:11008/v1/translate/<task_id>
```

## 3. MCP Server (`translate_pdf`)

Requires `pip install 'pdf2zh[mcp]'`. The MCP server exposes `translate_pdf(file, lang_in, lang_out)`, which accepts an absolute path to a `.pdf`, `.doc`, or `.docx` file and writes `<filename>-mono.pdf` and `<filename>-dual.pdf` alongside the source file.

### Run Modes

```bash
# STDIO transport (for Claude Desktop / Cursor / Antigravity MCP hosts)
pdf2zh --mcp

# SSE transport via CLI (default uvicorn host/port)
pdf2zh --mcp --sse

# SSE transport with explicit host/port via mcp_server module
python -m pdf2zh.mcp_server --sse --host 127.0.0.1 --port 3001
```

### Example `mcpServers` Client Config

```json
{
    "mcpServers": {
        "translate_pdf": {
            "command": "uv",
            "args": ["run", "pdf2zh", "--mcp"]
        }
    }
}
```
