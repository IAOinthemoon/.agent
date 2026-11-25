---
name: pdf-math-translate
description: >
  Translate scientific PDFs (and Word docs) while preserving original layouts, math formulas,
  figures, tables, TOC, and annotations using PDFMathTranslate (pdf2zh). Use when the user
  wants to translate a PDF paper into a monolingual or side-by-side bilingual PDF (mono/dual),
  install or configure pdf2zh CLI, select LLM/MT backends (OpenAI, DeepSeek, Gemini, Qwen-MT,
  Ollama, DeepL, Google, etc.), use --ultrafast or OCR modes, or connect pdf2zh via Python API,
  HTTP backend, or MCP server.
license: AGPL-3.0
---

# PDFMathTranslate (`pdf2zh`)

Translate scientific PDF documents (including arXiv URLs and `.doc`/`.docx` files) while preserving formulas, figures, tables, TOC, and annotations, producing both monolingual (`*-mono.pdf`) and bilingual (`*-dual.pdf`) PDFs.

Based on [PDFMathTranslate/PDFMathTranslate](https://github.com/PDFMathTranslate/PDFMathTranslate) (`pdf2zh` v1.9.12).

> **Choosing the right skill:**
> - Use **`pdf-math-translate`** when the user wants **layout-preserved translated PDFs** (`-mono.pdf` / `-dual.pdf`).
> - Use **[`academic-translation`](../academic-translation/SKILL.md)** when the user wants editable **Markdown / LaTeX / HTML** bilingual notes, deep three-step refinement (`直译 → 反思 → 雅化`), or arXiv `.tex` source translation.

## Workflow

### 1. Check or Install `pdf2zh`

`pdf2zh` requires **Python 3.11 or 3.12** (`>=3.11,<3.13`). First check if it is already installed:

```bash
command -v pdf2zh && pdf2zh --version
```

If missing, recommend/install according to the user's environment and needs:

```bash
# Recommended isolated CLI install (uv)
uv tool install --python 3.12 pdf2zh

# Or standard pip install
pip install pdf2zh
```

Optional extras (install only what is needed):
- **Ultrafast mode** (native-text PDFs, skips ONNX/OCR): `pip install 'pdf2zh[ultrafast]'`
- **Automatic OCR** (scanned image-only PDFs via PyMuPDF + Pooch): `pip install 'pdf2zh[ocr]'`
- **MCP server**: `pip install 'pdf2zh[mcp]'`
- **HTTP backend** (Flask + Celery + Redis): `pip install 'pdf2zh[backend]'`
- **GPU ONNX acceleration**: `pip install 'pdf2zh[cuda]'` (or `pdf2zh[dml]` on Windows DirectML)
- **Precise v2 kernel**: install `pdf2zh[precise]` and run `pdf2zh-setup-precise`

> **Model download mirror (restricted networks):** If downloading `wybxc/DocLayout-YOLO-DocStructBench-onnx` from HuggingFace fails, set `export HF_ENDPOINT=https://hf-mirror.com` before running `pdf2zh`.

### 2. Select Translation Service & Credentials

`pdf2zh` defaults to `-s google` (no key needed, quick layout test), but **LLM / dedicated MT backends** produce far better academic Chinese/English prose (`deepseek`, `openai`, `qwen-mt`, `gemini`, `zhipu`, `silicon`, `ollama`, `openailiked`, `deepl`, etc.).

1. Check whether `~/.config/PDFMathTranslate/config.json` or relevant environment variables (`DEEPSEEK_API_KEY`, `OPENAI_API_KEY`, `ALI_API_KEY`, etc.) already exist. Never echo or commit secret keys.
2. Specify service (and optional model) with `-s service` or `-s service:model`:
   ```bash
   pdf2zh paper.pdf -s deepseek
   pdf2zh paper.pdf -s openai:gpt-4o-mini
   ```
3. For OpenAI-compatible endpoints (`openai`, `grok`, `openailiked`), ensure `BASE_URL` ends with `/v1` (e.g., `https://api.openai.com/v1`), otherwise requests fail with HTTP 404.

Load [references/services-and-config.md](references/services-and-config.md) for the complete list of supported services, environment variables, `config.json` format, and custom `--prompt` usage.

### 3. Run PDF Translation

Common CLI invocations:

```bash
# Basic English → Simplified Chinese (outputs paper-mono.pdf & paper-dual.pdf)
pdf2zh paper.pdf -li en -lo zh -o ./output

# Translate directly from an online PDF URL (e.g., arXiv)
pdf2zh https://arxiv.org/pdf/2206.04655 -li en -lo zh -s deepseek -o ./output

# Preview / test first on specific pages before full-document API spend
pdf2zh paper.pdf -p 1-3,5 -s deepseek -o ./output

# Ultrafast heuristic mode for clean native-text PDFs (16 workers by default)
pdf2zh paper.pdf --ultrafast -li en -lo zh -s deepseek -o ./output

# Batch translate all PDF / Word files in a directory
pdf2zh --dir ./papers/ -li en -lo zh -o ./output
```

#### Key CLI Flags

| Flag | Purpose | Notes |
|---|---|---|
| `-li`, `-lo` | Source / target language codes | Defaults: `en` → `zh` (Google/DeepL codes) |
| `-s` | Translation service (`service[:model]`) | Default: `google` |
| `-o` | Output directory | Generates `<name>-mono.pdf` and `<name>-dual.pdf` |
| `-p` | Page selection (1-indexed), e.g., `1-3,5` | Test 1–2 pages first on long papers |
| `-t` | Worker threads | Default `4` (`16` with `--ultrafast`) |
| `--ultrafast` | Native-text heuristic layout (skips ONNX & OCR) | Cannot combine with `--mode precise`, `--babeldoc`, `--onnx`, or server/GUI modes |
| `--mode` | `fast` (v1 default) or `precise` (v2 experimental) | `precise` uses isolated env provisioned by `pdf2zh-setup-precise` |
| `--babeldoc` | Experimental BabelDOC typesetting backend | Alternative layout/rendering pipeline |
| `-f`, `-c` | Formula font / character regex preservation | Override if custom math fonts are misclassified |
| `--prompt` | Custom LLM prompt file (`${lang_in}`, `${lang_out}`, `${text}`) | System prompt not supported; pair with `--ignore-cache` when changing prompt |
| `--config` | Custom JSON config file path | Default path: `~/.config/PDFMathTranslate/config.json` |
| `--ignore-cache` | Bypass SQLite translation cache (`~/.cache/pdf2zh/cache.v1.db`) | Always pass after modifying `--prompt` or switching translation strategy |
| `--skip-subset-fonts` | Disable font subsetting | Larger file size, fixes missing/garbled glyph issues |
| `-cp` / `--compatible` | Convert output to PDF/A | Improves compatibility across PDF viewers |
| `-i` / `--serverport` | Launch Gradio WebUI | Only use when user explicitly requests local WebUI (default port `7860`) |

### 4. Programmatic, HTTP, or MCP Integration

If the user wants to embed `pdf2zh` into Python scripts, run an async HTTP translation server, or expose `translate_pdf` to an AI host via MCP (`pdf2zh --mcp` / `--sse`), read [references/api-and-mcp.md](references/api-and-mcp.md).

### 5. Verify Outputs & Troubleshoot

After running translation:
1. Verify both `<stem>-mono.pdf` and `<stem>-dual.pdf` exist in the output directory and have non-zero size.
2. Quick troubleshooting checklist:
   - **Scanned PDF produces blank/untranslated pages:** Install `pdf2zh[ocr]` (uses PyMuPDF built-in OCR; override language via `PDF2ZH_OCR_LANGUAGE=eng+deu` if needed) and avoid `--ultrafast`.
   - **Garbled characters or viewer fails to open PDF:** Re-run with `--skip-subset-fonts` and/or `--compatible`.
   - **Output unchanged after editing `--prompt` or service config:** Re-run with `--ignore-cache`.
   - **ONNX model download stalls:** Export `HF_ENDPOINT=https://hf-mirror.com`.
   - **Docker alternative (if Python 3.11/3.12 cannot be installed locally):** `docker pull byaidu/pdf2zh` (or `ghcr.io/byaidu/pdfmathtranslate`).
