# MIIRAI_CHAT — Student Getting Started

## What You'll Build
A local, multi-turn AI chat assistant with persistent memory that recalls past conversations, all running on your machine with Ollama.

## Prerequisites
- Python 3.10+
- Ollama with mistral:7b or llama3:8b

## Install
```bash
ollama pull mistral:7b
pip install miirai-chat
```

## First Working Example
```python
from miirai import Chat

chat = Chat(
    model="ollama/mistral:7b",
    system_prompt="You are Miirai, a helpful and concise assistant.",
    memory_backend="local_sqlite"
)

session = chat.new_session(user_id="student_001")
print(session.send("What is the Anticloud system?").text)
print(session.send("And what role does PAX play in it?").text)
print(f"Turns in session: {session.turn_count}")
```

## Add Persistent Memory Across Sessions
```python
from miirai import Chat

chat = Chat(model="ollama/mistral:7b", memory_backend="local_sqlite")
session = chat.new_session("alice")
session.send("My name is Alice and I'm studying distributed systems.")
session.end()

# New session — Miirai remembers Alice
new_session = chat.new_session("alice")
print(new_session.send("What was I studying?").text)
# Should recall: distributed systems
```

## Connect to a Knowledge Base
```python
from miirai import Chat
from kamelot import SearchIndex

index = SearchIndex(backend="local", embedding="nomic-embed-text")
index.build_from_directory("./course_notes/")

chat = Chat(model="ollama/mistral:7b", retrieval_backend=index)
session = chat.new_session("student")
print(session.send("Explain the concept from my notes about consensus algorithms").text)
```

## On Kaggle (loiskleinner account, T4 GPU)
```python
!pip install miirai-chat
!curl -fsSL https://ollama.ai/install.sh | sh
!ollama serve &
import time; time.sleep(5)
!ollama pull mistral:7b
```

## What's Next
- Try different system prompts and observe persona consistency
- Enable retrieval mode with your own document folder
- Connect to PAX_MATH_SOLVER for math question routing
