# Developer Cookbook — MIIRAI_CHAT
**Stack:** Python 3.11, FastAPI, WebSockets, SQLite, PAX 27B

## Python WebSocket client
```python
import asyncio, websockets, json

async def chat():
    async with websockets.connect("ws://localhost:8081/chat") as ws:
        await ws.send(json.dumps({"message": "How do I deploy K_BRAINFLOW air-gap?"}))
        resp = json.loads(await ws.recv())
        print(resp["text"], resp["chain_hash"])

asyncio.run(chat())
```

## Load conversation history
```python
from miirai_chat import MiiraiMemory
mem = MiiraiMemory("./miirai_memory.db")
history = mem.get_session("clinical_team_001")
for turn in history.turns[-10:]:
    print(f"[{turn.role}] {turn.content[:80]}")
```

## Compress long session
```python
summary = mem.summarize_session("clinical_team_001", pax_model="./pax-27b-q4.gguf")
print(summary.compressed_context)
```

## Performance
Compress turns older than 20 exchanges. SQLite FTS5 for history search.
Streaming WebSocket for low perceived latency.

## Integration
Uses KAMELOT_SEARCH for RAG. Feeds summaries into KANTOR_K5.
Used as backend by INTE11ECT_APP.
