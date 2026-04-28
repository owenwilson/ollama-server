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

### Edits below this comment will be discarded
```

```sh
sudo systemctl daemon-reload
sudo systemctl restart ollama
```

### check service

```sh
sudo cat /etc/systemd/system/ollama.service.d/override.conf
```

```sh
sudo ss -tulpn | grep ollama
```
