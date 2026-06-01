# 🤖 DecodeLabs — Project 1: Rule-Based AI Chatbot

> **Industrial Training Kit | Batch 2026 | Powered by DecodeLabs**

---

## 📌 Project Overview

This is **Project 1** of the DecodeLabs AI Industrial Training Kit — the foundation milestone every intern must complete before advancing to higher projects.

The goal is to build a **Rule-Based AI Chatbot** (ARIA — Adaptive Rule-based Intelligence Agent) that responds to predefined user inputs using pure **Control Flow and Logic** — no machine learning, no neural networks, just deterministic if-else decision-making through dictionary lookups.

---

## 🎯 Objectives

- Understand and implement the **IPO Model** (Input → Process → Output)
- Build a chatbot that runs in a **continuous loop**
- Apply **input sanitization** (lowercase + strip whitespace)
- Use a **Python dictionary / hash map** as the knowledge base (O(1) lookup)
- Handle **unknown inputs** with a fallback response
- Implement a clean **exit command** to break the loop

---

## 🗂️ Project Structure

```
decodelabs-project1/
│
├── decodelabs_chatbot.html     # Main chatbot application (web version)
├── chatbot.py                  # Python version of the chatbot
└── README.md                   # This file
```

---

## 🧠 Core Concepts Covered

| Concept | Description |
|---|---|
| **Control Flow** | `if-else` logic to route user inputs to responses |
| **Infinite Loop** | `while True` keeps the chatbot running until exit |
| **Input Sanitization** | `.lower().strip()` normalizes raw user input |
| **Dictionary / Hash Map** | O(1) lookup replaces slow O(n) if-elif ladders |
| **Fallback Handling** | `.get(key, default)` returns a default for unknowns |
| **Exit Strategy** | `break` statement gracefully ends the session |
| **IPO Model** | Input → Sanitize → Lookup → Match → Output |
| **White Box AI** | Every decision is traceable and explainable |

---

## 🏗️ Architecture

```
USER INPUT
    │
    ▼
┌─────────────────────┐
│   SANITIZATION      │  raw_input.lower().strip()
│   (Normalize)       │
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│   KNOWLEDGE BASE    │  Dictionary with 40+ intents
│   (Hash Map O(1))   │  { "hello": "Hi there!", ... }
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│   INTENT MATCHING   │  responses.get(clean_input, FALLBACK)
│   (.get() pattern)  │
└─────────┬───────────┘
          │
          ▼
┌─────────────────────┐
│   OUTPUT            │  Print response to user
│   (Feedback Loop)   │  → loop back to INPUT
└─────────────────────┘
```

---

## 🐍 Python Implementation

```python
# ══════════════════════════════════════════
# DecodeLabs — Project 1: Rule-Based Chatbot
# Author: [Your Name]
# Batch: 2026
# ══════════════════════════════════════════

# ── KNOWLEDGE BASE (Dictionary / Hash Map) ──
responses = {
    # Greetings
    "hello":        "Hello! I'm ARIA, your rule-based AI assistant. How can I help?",
    "hi":           "Hey there! Type 'help' to see what I can do.",
    "hey":          "Hey! What can I do for you today?",

    # Identity
    "who are you":  "I'm ARIA — a rule-based chatbot. No neural networks, pure logic!",
    "what are you": "I'm a deterministic AI. Same input always gives the same output.",

    # Help
    "help":         "I can answer: greetings, AI questions, jokes, motivation, and more!",

    # AI Concepts
    "what is ai":             "AI is the simulation of human intelligence in machines.",
    "what is machine learning": "ML is AI that learns from data — unlike me, I use hardcoded rules.",
    "what is deep learning":  "Deep Learning uses neural networks with many layers to find patterns.",

    # Jokes
    "tell me a joke": "Why don't programmers like nature? Too many bugs! 🐛",
    "joke":           "Why did the AI break up with the if-elif ladder? Too many conditions! 😄",

    # Motivation
    "motivate me":  "Every expert was once a beginner. You're building real AI today — keep going! 🚀",
    "i feel stuck": "Every bug is a lesson. Debug the logic, not yourself. You've got this!",

    # Farewell
    "bye":          "Goodbye! Keep building and keep learning. 👋",
    "goodbye":      "Farewell! Your AI journey has just begun.",
    "thanks":       "You're welcome! That's what rule-based systems are for.",
    "thank you":    "Happy to help! Mastering fundamentals is everything.",
}

# ── FALLBACK RESPONSE ──
FALLBACK = "I don't understand that. Try 'help' to see what I can respond to."


# ── MAIN CHATBOT FUNCTION ──
def chatbot():
    print("=" * 50)
    print("  ARIA — Rule-Based AI Chatbot")
    print("  DecodeLabs Project 1 | Batch 2026")
    print("=" * 50)
    print("Type 'exit' to end the session.\n")

    # ── INFINITE LOOP (heartbeat) ──
    while True:

        # PHASE 1: INPUT
        raw_input_text = input("You: ")

        # PHASE 2: SANITIZATION
        clean_input = raw_input_text.lower().strip()

        # EXIT STRATEGY — Kill command breaks the loop
        if clean_input in ["exit", "quit", "stop"]:
            print("ARIA: Goodbye! Session ended. Well done on completing Project 1! 🎉")
            break

        # PHASE 3: PROCESS — Dictionary lookup (O(1))
        reply = responses.get(clean_input, FALLBACK)

        # PHASE 4: OUTPUT
        print(f"ARIA: {reply}\n")


# ── ENTRY POINT ──
if __name__ == "__main__":
    chatbot()
```

---

## 🧪 Sample Interaction

```
==================================================
  ARIA — Rule-Based AI Chatbot
  DecodeLabs Project 1 | Batch 2026
==================================================
Type 'exit' to end the session.

You: hello
ARIA: Hello! I'm ARIA, your rule-based AI assistant. How can I help?

You: what is machine learning
ARIA: ML is AI that learns from data — unlike me, I use hardcoded rules.

You: tell me a joke
ARIA: Why don't programmers like nature? Too many bugs! 🐛

You: HELLO
ARIA: Hello! I'm ARIA, your rule-based AI assistant. How can I help?
(Note: sanitization converts 'HELLO' → 'hello' before lookup)

You: random nonsense
ARIA: I don't understand that. Try 'help' to see what I can respond to.

You: exit
ARIA: Goodbye! Session ended. Well done on completing Project 1! 🎉
```

---

## ⚡ Why Dictionary Over If-Elif?

| Approach | Time Complexity | Scalability | Maintainability |
|---|---|---|---|
| `if-elif` ladder | O(n) — linear | ❌ Slow with many rules | ❌ High technical debt |
| `dict.get()` | **O(1) — constant** | ✅ Instant regardless of size | ✅ Just add key-value pairs |

With 1,000 intents, an `if-elif` chain checks up to 1,000 conditions. A dictionary finds the answer in a **single operation** every time.

---

## 🛡️ Why Rule-Based AI Still Matters

Even in 2026, rule-based systems are used in production for critical reasons:

- **Traceability** — Every decision can be audited: Input → Logic → Output. No mystery.
- **Zero Hallucination Risk** — Responses are 100% hardcoded. No AI can "make something up."
- **Compliance** — Essential for Finance (FINRA), Healthcare (HIPAA), and Legal industries.
- **Speed** — O(1) lookup is faster than any LLM inference.
- **AI Guardrails** — Real-world LLM apps (NVIDIA NeMo, Llama Guard) use rule-based layers on top of probabilistic models. You just built that control layer.

---

## 🚀 How to Run

### Web Version
Simply open `decodelabs_chatbot.html` in any browser. No installation required.

### Python Version
```bash
# Make sure Python 3 is installed
python --version

# Run the chatbot
python chatbot.py
```

---

## 📈 Extending the Project (Bonus Ideas)

Want to go beyond the requirements and impress your reviewers? Try these:

1. **Add more intents** — Expand the knowledge base with 20+ more keys
2. **Partial matching** — Use `any(keyword in clean_input for keyword in keywords)` for flexible matching
3. **Conversation memory** — Store the last N messages and reference them in responses
4. **Multiple responses** — Use `random.choice([...])` so the bot doesn't always say the same thing
5. **Personality mode** — Add a `mode` variable that changes the bot's tone (formal / casual / sarcastic)
6. **Logging** — Write every exchange to a `.log` file for review
7. **Nested conditions** — Add sub-intents (e.g., ask a follow-up question after greeting)

---

## ✅ Project Checklist

Before submitting for badge verification, confirm all items:

- [ ] Chatbot runs in a **continuous `while True` loop**
- [ ] Input is **sanitized** with `.lower().strip()`
- [ ] Knowledge base is a **dictionary** with **5+ intents**
- [ ] Uses **`.get()` method** for O(1) lookup with fallback
- [ ] Has a **fallback response** for unrecognized inputs
- [ ] Has a clean **exit command** that breaks the loop
- [ ] Code is clean, commented, and readable
- [ ] Tested with multiple inputs including edge cases

---

## 👤 Author

| Field | Details |
|---|---|
| **Name** | [Your Name] |
| **Batch** | DecodeLabs 2026 |
| **Project** | Project 1 — Rule-Based AI Chatbot |
| **Track** | Artificial Intelligence Engineering |
| **Organization** | DecodeLabs, Greater Lucknow, India |

---

## 📬 Contact DecodeLabs

| Channel | Details |
|---|---|
| 📞 Phone | +91 89330 06408 |
| ✉️ Email | decodelabs.tech@gmail.com |
| 🌐 Website | www.decodelabs.tech |
| 📍 Location | Greater Lucknow, India |

---

> *"An LLM without rules is a hallucination engine. Today, we build the skeleton that holds the intelligence."*
> — DecodeLabs Architecture Briefing, Module 01

---

**Project 1 Complete. Your AI engineering journey has begun. 🚀**
