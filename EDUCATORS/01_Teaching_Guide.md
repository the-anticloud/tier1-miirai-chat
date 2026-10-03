# MIIRAI_CHAT — Educator's Teaching Guide

## Course Fit: conversational AI, chatbot design, LLM deployment, human-AI interaction

## 3-Week Module: Sovereign Conversational AI Systems

### Week 1: Conversational AI Architecture
**Lecture Topics:**
- Stateful vs. stateless chat: why context management is hard
- MIIRAI_CHAT's design: local inference, persistent memory, multi-turn coherence
- System prompt engineering for consistent persona
- Conversation state machines: turn, session, long-term memory

**Lab Exercise:**
```python
from miirai import Chat, Session
chat = Chat(model="ollama/mistral:7b",
            system_prompt="You are Miirai, a helpful sovereign AI assistant.",
            memory_backend="local_sqlite")
session = chat.new_session(user_id="student_001")
response = session.send("What is the Anticloud system?")
print(response.text)
response2 = session.send("And how does PAX fit into it?")
print(response2.text)
print(f"Session context tokens: {session.context_tokens}")
```

### Week 2: Memory, Retrieval, and Personalization
**Lecture Topics:**
- Episodic memory: storing conversation summaries for long-term recall
- Semantic memory: user preferences, facts, and knowledge
- Retrieval-augmented conversation: pulling from KAMELOT_SEARCH
- Safety and moderation in local deployments

**Lab Exercise:**
```python
from miirai import Chat, EpisodicMemory
memory = EpisodicMemory(db="miirai_memory.db", summary_model="ollama/llama3:8b")
chat = Chat(model="ollama/mistral:7b", memory=memory)
session = chat.new_session("user_alice")
for _ in range(10):
    session.send("Tell me about distributed systems")
memory.summarize_session(session.id)
new_session = chat.new_session("user_alice")
print(new_session.recall_context())  # should include prior session summary
```

### Week 3: MIIRAI_CHAT in the Anticloud Ecosystem
**Lecture Topics:**
- MIIRAI as the user-facing layer over KAMELOT_SEARCH, PAX, and INTE11ECT_APP
- AIOSS logging of conversation sessions for enterprise compliance
- Multi-model routing: math queries to PAX_MATH_SOLVER, code to ANTICODE_AGENT
- Deployment in SOVEREIGN_OS with LIBERN_PLATFORM rate limiting

**Lab Exercise:**
```python
from miirai import Chat
from pax_client import PAXRouter
router = PAXRouter({"math": "pax_math", "code": "anticode_agent"})
chat = Chat(model="ollama/mistral:7b", router=router)
session = chat.new_session("user_bob")
print(session.send("What is the integral of x^3?").text)
print(session.send("Write a quicksort in Python").text)
```

## Exam Questions
1. Describe the difference between episodic and semantic memory in a chat system. Give an example of each in the context of MIIRAI_CHAT.
2. How does retrieval-augmented conversation improve over pure in-context learning? What happens when the retrieved document contradicts the model's parametric knowledge?
3. Design a safety policy for MIIRAI_CHAT deployed in a university setting. What categories of content would you filter, and how would you implement filtering without cloud API calls?
