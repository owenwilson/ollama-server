# ollama server local network

### setup

- install ollama on linux, [please refer to the documentation for installation instructions](https://ollama.com/)
- install [cline extension on your vscode](https://marketplace.visualstudio.com/items?itemName=saoudrizwan.claude-dev)

```sh
sudo systemctl status ollama
```

- edit ollama service

```sh
sudo systemctl edit ollama
```

- add the following lines

```sh
[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
Environment="OLLAMA_KEEP_ALIVE=-1s"
Environment="OLLAMA_NUM_PARALLEL=1"
Environment="OLLAMA_LOAD_TIMEOUT=10m"

### Edits below this comment will be discarded
```

```sh
sudo systemctl daemon-reload
sudo systemctl restart ollama
```

### test service

```sh
curl http://IP_DEL_SERVIDOR_LINUX:11434/api/generate -d '{
  "model": "qwen2.5:latest",
  "prompt": "Hi, What is your name.",
  "stream": false
}'
```
### check service

```sh
sudo cat /etc/systemd/system/ollama.service.d/override.conf
```

```sh
sudo ss -tulpn | grep ollama
```

```sh
curl http://[IP_DEL_SERVIDOR_LINUX]:11434
```

### revert ollama service

```sh
sudo systemctl revert ollama
```

## Modefile

- create a modified version of the model with a broader context using a Modefile

```sh
FROM qwen2.5-coder:14b
PARAMETER num_ctx 32768
```
- build new model

```sh
ollama create qwen2.5-coder-14b-32k -f Modefile
```

## vscode

- configuration file of continue.dev

```sh
~/.continue/config.yaml
```

- example config.yaml

```sh
name: Main Config
version: 1.0.0
schema: v1
models:
  - name: Qwen2.5 Coder 14B (Remote)
    provider: ollama
    model: qwen2.5-coder-14b-32k
    apiBase: http://IP:11434
    roles:
      - chat
      - edit
      - apply
  - name: Qwen2.5-Coder 1.5B
    provider: ollama
    model: qwen2.5-coder:1.5b-base
    roles:
      - autocomplete
  - name: Nomic Embed
    provider: ollama
    model: nomic-embed-text:latest
    roles:
      - embed
```

## references

- check out [continue dev](https://continue.dev/)
- check out [ide extension](https://docs.continue.dev/ide-extensions/quick-start)
- check out [continue dev models](https://docs.continue.dev/customize/models)
- check out [modelfile](https://docs.ollama.com/modelfile)
