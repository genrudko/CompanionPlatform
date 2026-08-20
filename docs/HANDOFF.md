# Companion Platform — Handoff

## Purpose

Companion Platform is a personal engineering continuity system connecting human, AI assistant and real engineering infrastructure.

The main problem:
- chat sessions are temporary;
- decisions remain inside conversations;
- manual handoff is required.

The goal is persistent engineering state independent from a specific chat session.

## Origin

The project started from experiments connecting ChatGPT Plus with an X96 Companion box.

Explored:
- SSH access;
- MCP bridge;
- local tool execution.

Conclusion:
MCP provides tool access, but does not solve persistent memory.

## Architecture

Human
→ ChatGPT Plus / LLM
→ Companion Core
→ OS adapters (Linux / Windows / Android)

Plus evidence storage.

## Principles

LLM provides reasoning, planning and communication.

Companion Core stores:
- state;
- projects;
- events;
- decisions;
- evidence.

OS layer provides execution.

## MVP

Initial Core:
- state database;
- project registry;
- event log;
- decision storage;
- API;
- git integration;
- OpenRouter connector.

Next step:
Design Companion Core.
