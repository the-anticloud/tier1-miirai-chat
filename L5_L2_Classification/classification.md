# L5 Narrow / L2 General Classification — MIIRAI_CHAT
**Platform:** Anticloud | **PAX:** 27B | **IP:** USPTO pending 2026, Anticloud FZ LLE

## L5 Narrow
MIIRAI_CHAT specializes in persistent multi-turn conversations about Anticloud deployment contexts:
technical ops questions, clinical AI queries, robotics debugging. No social chatbot, no general
trivia. Conversation memory compressed via KAMELOT_SEARCH retrieval, not cloud sync.

## L2 General
Universal conversational interface for any Anticloud deployment team: hospital clinical staff,
defense engineers, robotics operators. Same interface, domain-specific routing.

## PAX Integration
PAX 27B generates all responses. MIIRAI_CHAT manages context windowing (compress old turns via
summarization), submits current context to PAX, streams response, chains each turn.

## AIOSS Audit Relevance
Every conversation turn (user message hash + assistant response hash + session ID) is chained.
Compliance-ready: auditors can verify conversation contents without cloud logs.

## Regulatory
GDPR Art. 5 (data minimisation, local storage only), CCPA 1798.100, ISO/IEC 27701
