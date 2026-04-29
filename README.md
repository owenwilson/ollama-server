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
Environment="OLLAMA_HOST=0.0.0.0"
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
