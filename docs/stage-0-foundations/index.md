---
tags:
  - foundations
  - stage-0
  - prompt-engineering
  - llm-basics
---

# Stage 0 — Foundations: Talk to an LLM Through Code

> **Goal:** Send your first message to a language model from your own code, get a response back, and understand exactly what happened in between.

This is where the roadmap stops being theory. By the end of Stage 0 you'll have a working chatbot you built yourself — and, more importantly, a mental model of what an LLM actually *is* from an engineer's seat: a function you call over the internet that takes text and returns text.

## What actually happens when you "talk" to an LLM

Every interaction, no matter how fancy the app, is the same loop underneath:

```mermaid
graph LR
    A["Your code builds<br/>a list of messages"] --> B["Send request<br/>to the API"]
    B --> C["Model processes<br/>the tokens"]
    C --> D["Response streams<br/>back as text"]
    D --> E["Your code displays<br/>or uses it"]
    E -.->|"add reply, repeat"| A
```

There's no magic. You assemble some text, send it, and get text back. Everything you build later — RAG, agents, all of it — is a more sophisticated version of this exact loop.

## The concepts you'll learn here

### Messages and roles

An LLM conversation isn't one blob of text. It's a **list of messages**, each with a role:

- **System** — the instructions that set the model's behavior ("You are a helpful tutor"). The user usually doesn't see this.
- **User** — what the person types.
- **Assistant** — what the model replied. You send past replies back so the model "remembers" the conversation.

The model has no memory of its own. **You** rebuild the whole conversation and send it every single time. That realization is the foundation of everything.

### Tokens

Models don't read words — they read **tokens**, chunks of text roughly ¾ of a word. "Engineering" might be two tokens. Why you care:

- **You're billed per token** — input *and* output.
- Tokens are the unit behind every limit and every cost. Watch them from day one.

### Context window

The **context window** is the maximum number of tokens the model can consider at once — its short-term memory. Exceed it and the earliest messages fall off. Long conversations, big documents, and cost all run into this ceiling. Managing it is a real part of the job.

### Temperature

**Temperature** controls randomness. Low (near 0) = focused and repeatable; higher = more creative and varied. Same prompt, different temperature, different answer. Use low for extraction and code, higher for brainstorming.

### Streaming

Instead of waiting for the full reply, **streaming** returns tokens as they're generated — the "typing" effect you see in chat apps. It makes your app feel fast and is worth wiring in early.

### Prompt engineering (the real leverage)

How you ask changes what you get. The core moves:

- **Be specific.** Vague prompt, vague answer.
- **Zero-shot vs few-shot.** Give examples when you want a specific format or style.
- **Role prompting.** "You are an expert Python reviewer…" shapes the output.
- **Ask for structure.** Tell it to reply in JSON when you need machine-readable output.
- **Chain-of-thought.** "Think step by step" improves reasoning on harder tasks.

## Build it: your first three projects

Learning sticks when you ship. Do at least the first one.

### Project 1 — CLI Chatbot *(do this one)*

A terminal chatbot that holds a conversation, remembers context, and streams replies.

**Hand this to Claude Code:**

```
Build a command-line chatbot in Python that talks to an LLM API.

Requirements:
- A loop that reads my input in the terminal and prints the model's reply.
- Maintain conversation history so the model remembers earlier turns
  (send the full message list each request).
- Include a configurable system prompt at the top of the file.
- Stream the response so it prints token-by-token like a typing effect.
- Type "exit" to quit; type "reset" to clear the conversation history.
- Load the API key from an environment variable, never hard-coded.
- Add a short README explaining, for a beginner, how the message list and
  streaming work.
Keep it to a single, well-commented Python file plus the README.
```

**What it teaches:** messages/roles, conversation memory, streaming, API keys — the whole Stage 0 loop in one artifact.

### Project 2 — Structured Extractor

Feed in messy text (a review, an email) and get back clean JSON: sentiment, key points, action items. Teaches prompting for *reliable structure* and low temperature.

### Project 3 — Prompt Playground

A tiny web UI (Streamlit or Gradio) where you tweak the system prompt and temperature and compare outputs side by side. Teaches how much prompt and settings actually change results.

## You're done with Stage 0 when…

- [ ] You have a working chatbot you built and understand line by line.
- [ ] You can explain why the model "remembers" only what you resend.
- [ ] You can force valid JSON output from a prompt.
- [ ] You can explain how temperature changes an answer.

## What's next

You've got a model that's smart but knows nothing about *your* world. **Stage 1 — RAG** fixes that: you'll give the model your own documents and have it answer questions using them, with citations. That's where AI engineering starts to feel like a superpower.

*Part 2 of the AI Engineering Roadmap. Built in public — every concept ships with a project you can build yourself.*
