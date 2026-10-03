# Miirai — The Sovereign Companion AI

**Status:** Production-ready | **Version:** 1.0.0 | **Author:** Lois-Kleinner Alpasan  
**Model:** SmolLM2-360M (obfuscated, quantum-ready)  
**Platform:** Desktop (Tauri) + Mobile (iOS/Android)

---

## What Is Miirai?

Miirai (みいらい — "future of self") is a 0.5B parameter sovereign AI companion designed for offline, CPU-only deployment on outdated devices. It is AGI-like in UX, privacy-first by architecture, and cryptographically auditable through AIOSS ledger integration.

Miirai stands alone as a complete AI system but is strengthened by integration with AIOSS (for audit trail), K5 (for quantum-resistant hashing), and Inte11ect (for multi-expert reasoning).

---

## Key Features

### AI Capabilities
- **360M parameters** (SmolLM2 base, obfuscated for brand independence)
- **Offline inference** — All computation on-device, no cloud
- **4 inference engines:**
  - Standard generation
  - RAG (Retrieval-Augmented Generation) with 9 knowledge bases
  - Contradiction detection (checks prior memory for inconsistencies)
  - Red-teaming (attacks own output for hallucinations)
- **Confidence scoring** — Every response includes confidence bars
- **Follow-up suggestions** — 3 contextual follow-up questions

### User Experience
- **Desktop:** Tauri single-binary app (Windows, macOS, Linux)
- **Mobile:** Native iOS + Android shells via Tauri
- **UI:** React 18 + TypeScript + Tailwind CSS
- **Rich text:** Markdown rendering with syntax highlighting
- **Conversation history:** Local SQLite with full-text search

### Privacy & Security
- **No telemetry** — Zero data sent anywhere
- **Encrypted storage** — Messages in encrypted SQLite
- **AIOSS ledger** — Cryptographic audit of every interaction
- **Ed25519 signing** — Every inference digitally signed
- **Recovery codes** — 24-word BIP39 seed for device recovery

### Orchestration
- **Sliders for personality:** Warmth (0-100), Creativity (0-100), Focus (0-100), Formality (0-100), Verbosity (0-100)
- **Adjusts in real-time** — Model output shaped by slider positions
- **Reproducible** — Same sliders + prompt = same response

---

## Architecture

```
┌─────────────────────────────┐
│   Desktop/Mobile UI         │
│ (Tauri + React)             │
└──────────────┬──────────────┘
               │
        ┌──────▼──────────────────────┐
        │  Miirai Orchestrator Layer  │
        │  (warmth, creativity, etc)  │
        └──────┬─────────────────────┘
               │
   ┌───────────┼───────────┬──────────────┬─────────────┐
   │           │           │              │             │
   ▼           ▼           ▼              ▼             ▼
Inference   RAG Engine  Contradiction  Red Team    Response
Engine      (9 KB)      Engine         Engine      Synthesis
   │           │           │              │
   └───────────┴───────────┴──────────────┴─────────────┐
                           │
                    ┌──────▼──────────┐
                    │ AIOSS Ledger    │
                    │ (SHA3-256 chain)│
                    │ (K5 ready)      │
                    └─────────────────┘
                           │
                    ┌──────▼──────────┐
                    │  Persistence    │
                    │ • SQLite (chat) │
                    │ • Qdrant (RAG)  │
                    │ • GGUF (model)  │
                    └─────────────────┘
```

---

## Quick Start

```bash
# Desktop (macOS/Windows/Linux)
./Miirai.app  # or miirai.exe, miirai on Linux

# Mobile
# iOS: Download from App Store (coming 2026)
# Android: Download from Play Store (coming 2026)

# CLI (optional, for advanced users)
miirai-cli --prompt "What's the best way to learn Rust?"
miirai-cli --rag-mode --prompt "Medical advice for a fever"
miirai-cli --contradiction-check "I previously said X, now say Y"
```

---

## Use Cases

### 1. Personal Knowledge Assistant
- Store personal notes, documents
- Ask questions across all knowledge
- Offline, encrypted, private

**Example:** Store medical history → Ask "What symptoms suggest I'm allergic to X?"

### 2. Medical Companion (with disclaimers)
- 9 knowledge bases: anatomy, pharmacology, diagnostics, etc.
- RAG retrieves relevant medical knowledge
- Red-team checks for dangerous hallucinations
- **Important:** Always consult qualified doctor for actual medical decisions

**Example:** "How to treat a minor burn at home?" → RAG retrieves burn treatment guides → Red-team verifies accuracy → Response with confidence score

### 3. Learning & Tutoring
- Tutor across any subject (math, language, history, coding)
- Adjustable difficulty via sliders
- Confidence scoring on correctness
- Reproducible explanations (same sliders = same explanation)

**Example:** Set (Formality=80, Verbosity=50) for professional explanations; Set (Warmth=90, Verbosity=80) for encouraging beginner tutoring

### 4. Code Assistant
- Local code generation (no code sent to cloud)
- Syntax highlighting, formatting
- Integration with editor (VS Code plugin coming)

**Example:** "Write a Rust function to hash a K5 sponge state"

### 5. Offline Diary & Reflection
- Private journaling with AI reflection
- Mood tracking, goal setting
- All encrypted, never leaves device

**Example:** "I'm anxious about upcoming presentation" → Miirai suggests coping strategies → Confidence: 85%

---

## Model Specifications

| Property | Value |
|----------|-------|
| Base Model | SmolLM2-360M (Alibaba Qwen team) |
| Parameter Count | 360 million |
| Quantization | FP8 (efficient, ~450MB GGUF) |
| Context Length | 4096 tokens (configurable) |
| Inference Speed | ~5-8 tokens/second (CPU) |
| Memory Required | ~1.5GB (model) + 200MB (KV cache) |
| Power Draw | ~25W typical |
| Energy per Query | ~25-75 Joules |

---

## Knowledge Bases (RAG)

Miirai ships with 9 knowledge bases:

1. **Medical** — Common conditions, treatments, diagnostics
2. **Pharmacology** — Drug interactions, side effects
3. **Anatomy** — Human body systems
4. **Nutrition** — Food, diets, health guidelines
5. **Psychology** — Mental health, coping strategies
6. **Science** — Physics, chemistry, biology fundamentals
7. **History** — World history, events, figures
8. **Technology** — Computing, AI, software engineering
9. **Business** — Economics, management, entrepreneurship

Users can add custom knowledge bases (PDFs, markdown, text files).

---

## Integration with Other Projects

### AIOSS (Audit Trail)
Every inference automatically appended to AIOSS ledger:
```
User prompt → SHA3-256 hash
     ↓
Model output → SHA3-256 hash
     ↓
AIOSS entry: (prompt_hash || output_hash || timestamp || confidence)
     ↓
Hash chain: H(prev || current)
     ↓
Cryptographic proof nothing was altered
```

### K5 (Post-Quantum Hash)
Optional migration from SHA3-256 to K5-512:
```yaml
# miirai config
ledger:
  hash_function: "k5-512"  # was: "sha3-256"
  quantum_resistant: true
```

### MF+SO (Identity)
Sign inference ledger with MF+SO Ed25519 keys:
```python
identity = mfso.get_user_identity()
signature = mfso.sign(inference_hash)
aioss.append(
  actor=identity,
  signature=signature,
  content=inference_result
)
```

### Inte11ect (Multi-Expert Reasoning)
Optional: Route complex queries to Inte11ect's 71 expert modules:
```python
if complexity_score > 0.7:
    # Route to Inte11ect for expert analysis
    result = inte11ect.query_experts(prompt)
else:
    # Use Miirai directly
    result = miirai.generate(prompt)
```

---

## Privacy

- **No cloud connectivity** — All inference on-device
- **No telemetry** — Zero analytics sent anywhere
- **Encrypted storage** — Conversation history encrypted with XChaCha20-Poly1305
- **Device recovery** — 24-word BIP39 seed enables device recovery
- **AIOSS auditing** — User controls their own audit trail (never shared)

---

## Limitations

- **360M parameters** — Smaller than cloud models (GPT-4 is 1.7T+)
- **CPU-only** — Not real-time speed; ~5-8 tokens/second
- **No vision** — Text-only; no image input or output
- **No internet** — Cannot browse or fetch real-time data
- **Heuristic RAG** — Knowledge bases are curated, not learned
- **No code sandbox** — Generated code is text-only, not executed

---

## License

MIT — Lois-Kleinner Alpasan

---

## References

1. Lois-Kleinner Zenodo: https://doi.org/10.5281/zenodo.20781790
2. GitHub: https://github.com/kleinnner/Anticloud
3. ORCID: https://orcid.org/0009-0009-2233-6107
