# Translation Services, Configuration & Custom Prompts

Reference compiled from [PDFMathTranslate `docs/ADVANCED.md`](https://github.com/PDFMathTranslate/PDFMathTranslate/blob/main/docs/ADVANCED.md) and `pdf2zh/pdf2zh.py`.

## Supported Translation Services (`-s`)

| Translator | `-s` Value | Required Environment Variables | Default Values / Notes |
|---|---|---|---|
| **Google (Default)** | `google` | None | Free machine translation |
| **Bing** | `bing` | None | Free machine translation |
| **DeepSeek** | `deepseek` | `DEEPSEEK_API_KEY`, `DEEPSEEK_MODEL` | Default model: `deepseek-chat` |
| **OpenAI** | `openai` | `OPENAI_BASE_URL`, `OPENAI_API_KEY`, `OPENAI_MODEL`, `OPENAI_STOP_TOKENS`, `OPENAI_MAX_TOKENS` | Defaults: `https://api.openai.com/v1`, `gpt-4o-mini` |
| **Ali Qwen MT** | `qwen-mt` | `ALI_API_KEY`, `ALI_MODEL`, `ALI_DOMAINS` | Defaults: `qwen-mt-turbo`, domain `scientific paper` (Simplified Chinese) |
| **Gemini** | `gemini` | `GEMINI_API_KEY`, `GEMINI_MODEL` | Default: `gemini-1.5-flash` |
| **Zhipu** | `zhipu` | `ZHIPU_API_KEY`, `ZHIPU_MODEL` | Default: `glm-4-flash` |
| **SiliconFlow** | `silicon` | `SILICON_API_KEY`, `SILICON_MODEL` | Default: `Qwen/Qwen2.5-7B-Instruct` |
| **ModelScope** | `modelscope` | `MODELSCOPE_API_KEY`, `MODELSCOPE_MODEL` | Default: `Qwen/Qwen2.5-Coder-32B-Instruct` |
| **MiniMax** | `minimax` | `MINIMAX_API_KEY`, `MINIMAX_MODEL` | Default: `MiniMax-M2.7` |
| **Grok** | `grok` | `GROK_API_KEY`, `GROK_MODEL`, `GROK_BASE_URL` (opt) | Default: `grok-2-1212`, `https://api.x.ai/v1` |
| **Groq** | `groq` | `GROQ_API_KEY`, `GROQ_MODEL` | Default: `llama-3-3-70b-versatile` |
| **302.AI** | `302ai` | `X302AI_API_KEY`, `X302AI_MODEL` | Default: `Gemma-7B` |
| **Azure OpenAI** | `azure-openai` | `AZURE_OPENAI_BASE_URL`, `AZURE_OPENAI_API_KEY`, `AZURE_OPENAI_MODEL` | Default: `gpt-4o-mini` |
| **OpenAI-Compatible** | `openailiked` | `OPENAILIKED_BASE_URL`, `OPENAILIKED_API_KEY`, `OPENAILIKED_MODEL` (+ opt `OPENAILIKED_STOP_TOKENS`, `OPENAILIKED_MAX_TOKENS`) | Any OpenAI-compatible API; `BASE_URL` **must end with `/v1`** |
| **Ollama (Local)** | `ollama` | `OLLAMA_HOST`, `OLLAMA_MODEL` | Defaults: `http://127.0.0.1:11434`, `gemma2` |
| **Xinference (Local)** | `xinference` | `XINFERENCE_HOST`, `XINFERENCE_MODEL` | Defaults: `http://127.0.0.1:9997`, `gemma-2-it` |
| **DeepL** | `deepl` | `DEEPL_AUTH_KEY` | Official DeepL API |
| **DeepLX** | `deeplx` | `DEEPLX_ENDPOINT` | Default: `https://api.deepl.com/translate` |
| **Azure Translator** | `azure` | `AZURE_ENDPOINT`, `AZURE_API_KEY` | Default endpoint: `https://api.translator.azure.cn` |
| **Tencent TMT** | `tencent` | `TENCENTCLOUD_SECRET_ID`, `TENCENTCLOUD_SECRET_KEY` | Tencent Cloud machine translation |
| **Argos Translate** | `argos` | None | Offline open-source MT (`pip install 'pdf2zh[argostranslate]'`) |
| **Dify** | `dify` | `DIFY_API_URL`, `DIFY_API_KEY` | Requires workflow inputs `lang_out`, `lang_in`, `text` |
| **AnythingLLM** | `anythingllm` | `AnythingLLM_URL`, `AnythingLLM_APIKEY` | AnythingLLM workspace integration |

## Custom Configuration File (`--config`)

Default config location: `~/.config/PDFMathTranslate/config.json`. Environment variables take precedence over `config.json` when both are set.

```json
{
    "USE_MODELSCOPE": "0",
    "PDF2ZH_LANG_FROM": "English",
    "PDF2ZH_LANG_TO": "Simplified Chinese",
    "NOTO_FONT_PATH": "/path/to/SourceHanSerifCN-Regular.ttf",
    "translators": [
        {
            "name": "ollama",
            "envs": {
                "OLLAMA_HOST": "http://127.0.0.1:11434",
                "OLLAMA_MODEL": "gemma2"
            }
        },
        {
            "name": "openailiked",
            "envs": {
                "OPENAILIKED_BASE_URL": "https://api.example.com/v1",
                "OPENAILIKED_API_KEY": "your-api-key",
                "OPENAILIKED_MODEL": "your-model"
            }
        }
    ]
}
```

## Custom LLM Prompt (`--prompt`)

Pass a template file with `--prompt prompt.txt` (always add `--ignore-cache` when iterating on prompts). System prompts are not supported; available template variables are `${lang_in}`, `${lang_out}`, and `${text}`:

```text
You are a professional, authentic machine translation engine. Only output the translated text, do not include any other text.

Translate the following markdown source text from ${lang_in} to ${lang_out}. Keep the formula notation {v*} unchanged. Output translation directly without any additional text.

Source Text: ${text}

Translated Text:
```

## Formula Preservation Regex (`-f`, `-c`)

Default formula font preservation regex:

```bash
pdf2zh example.pdf -f "(CM[^R]|MS.M|XY|MT|BL|RM|EU|LA|RS|LINE|LCIRCLE|TeX-|rsfs|txsy|wasy|stmary|.*Mono|.*Code|.*Ital|.*Sym|.*Math)"
```

Custom font (`-f`) and character (`-c`) override example:

```bash
pdf2zh example.pdf -f "(CM[^RT].*|MS.*|.*Ital)" -c "(\(|\||\)|\+|=|\d|[\u0080-\ufaff])"
```
