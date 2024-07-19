Im Stammverzeichnis habe ich einen Node-Container gestartet:

```bash
docker run -it --rm -v $(pwd):/app -p 5173:5173 -w/app  node:iron-alpine3.20 /bin/sh
```

Dort erzeuge ich die Vue-Application "frontend" mit

```bash
npm create vue@latest
# Ausfüllen der Fragen ... Project name: frontend ...
cd frontend
npm install
```

Jetzt habe ich den Container verlassen und die Dockerfile für das Frontend im Verzeichnis Frontend sowie die compose.yaml im Stammverzeichnis erstellt.

Anpassung in `package.json`: `"dev": "vite --host"`. Hier wurde "host" hinzugefügt. Optional geht auch
noch zusätzlich `--port 80`, um das Frontend gleich auf Port 80 laufen zu lassen und nicht erst noch auch
Standard 5173. Jetzt habe ich das Frontend starten können:

```bash
docker compose up frontend
```
