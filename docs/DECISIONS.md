# Companion Platform — Decision Log

## D-001 — Companion is separate from ChatGPT

Accepted.

LLM providers are intelligence clients. Companion Core stores persistent state.

## D-002 — LLM is not source of truth

Source of truth:
- repositories;
- files;
- tests;
- runtime state;
- Companion database.

## D-003 — Evidence-based memory

Important decisions require evidence:
- commits;
- files;
- tests;
- discussion context.

## D-004 — Separate Core and interfaces

Interfaces:
- ChatGPT Bridge;
- Desktop Client;
- Android Client;
- CLI.

## D-005 — ChatGPT Plus remains important

Goal is integration, not replacement.

## D-006 — OpenRouter is auxiliary

Used for:
- summaries;
- automation;
- background analysis.

## D-007 — Human remains final authority

AI assists but does not silently replace engineering decisions.

## D-008 — Core first

Build state and memory before UI.
