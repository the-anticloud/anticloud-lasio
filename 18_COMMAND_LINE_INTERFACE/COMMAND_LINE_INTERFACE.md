# Command Line Interface — LASIO

**Upstream:** https://github.com/kinverarity1/lasio

## Anticloud CLI

```bash
# Install
pip install anticloud-lasio

# Run offline with PAX inference
anticloud-lasio --offline --pax-local

# Run with AIOSS logging
anticloud-lasio --aioss-log ./ledger.jsonl

# Single binary (after build)
./lasio --config config.yaml
```

## Options

| Flag | Description |
| --- | --- |
| `--offline` | Disable all network calls |
| `--pax-local` | Use local PAX inference at 127.0.0.1:11434 |
| `--aioss-log PATH` | Write AIOSS audit chain to PATH |
| `--encrypt` | Enable AES-256 at rest for output files |
| `--gpu` | Force GPU inference |
| `--cpu` | Force CPU inference |
| `--config PATH` | Load configuration from YAML file |
