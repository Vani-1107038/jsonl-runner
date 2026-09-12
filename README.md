# jsonl-runner

Batch prompt runner with real rate limiting and retries

## Getting started

```bash
pip install -r requirements.txt
export OPENAI_API_KEY=sk-...
```

## Examples

```bash
python batch.py prompts.jsonl -o answers.jsonl --workers 4 --rpm 300
```

## Highlights

- Idempotent: ids already in the output are skipped on a rerun
- A bad input line is logged and skipped, never fatal
- Per-row overrides for model, system, temperature and max_tokens
- Real rate limiting: sliding windows on requests/min and tokens/min
- JSONL in, JSONL out: the input is streamed line by line
- 4xx fails fast; 429 and 5xx retry with jittered backoff
- Progress, token counts and a cost estimate on stderr
- Failures go to a sidecar file with error type, message and status

## Project structure

```text
├── .github/
│   ├── workflows/
│   │   └── ci.yml
│   └── dependabot.yml
├── docs/
│   ├── configuration.md
│   ├── development.md
│   ├── roadmap.md
│   ├── tradeoffs.md
│   └── usage.md
├── examples/
│   └── quickstart.md
├── tests/
│   └── test_smoke.py
├── .gitignore
├── CHANGELOG.md
├── CONTRIBUTING.md
├── LICENSE
├── batch.py
├── prompts.sample.jsonl
└── requirements.txt
```

## Development

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m pytest -q
```

## FAQ

**Is this production ready?**  
It works for my use case; review the code before relying on it.

**Why no framework?**  
The stdlib covers what this project needs.

## License

MIT - see [LICENSE](LICENSE).
