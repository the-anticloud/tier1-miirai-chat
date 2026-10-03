# Deploy Guide — MIIRAI_CHAT
## Prerequisites
- Python 3.11+, FastAPI 0.110+, websockets 12.0+, SQLite (stdlib), PAX 27B

## Environment
- 16GB RAM. GPU optional. WebSocket server on localhost:8081. SQLite for conversation store.

## Install
```bash
pip install anticloud-miirai fastapi uvicorn websockets
```

## Start chat server
```bash
python -m miirai_chat --model ./pax-27b-q4.gguf --port 8081 --memory ./miirai_memory.db --aioss ./chat.aioss
```

## Air-Gap
All conversation stored locally in SQLite. No cloud sync. Fully offline.

## Verification
```bash
curl http://localhost:8081/health
aioss verify --chain ./chat.aioss
```
