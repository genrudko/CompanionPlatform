# Companion Platform — Storage Model

## Purpose

This document defines how Companion Core stores persistent information.

The storage model follows the principle that historical facts, structured knowledge and current operational state are different layers.

---

# Storage principles

## Immutable history

Some data represents facts and should not be overwritten.

Examples:

- Events;
- Archive items;
- Evidence.

Corrections create new records instead of rewriting history.

---

## Structured memory

Structured objects represent interpreted knowledge.

Examples:

- Decisions;
- WorkItems;
- Relationships between entities.

They may evolve, but previous states remain traceable.

---

## Operational state

Current state is a working projection used for daily operation.

It can be regenerated from historical data and structured memory.

---

# Initial storage backend

MVP target:

SQLite.

Reasons:

- single portable database file;
- suitable for VPS, desktop and embedded systems;
- easy backup and migration;
- no additional database service required.

---

# Core entities

## Project

Stores project identity.

Fields:

- id;
- name;
- description;
- timestamps.

---

## Workspace

Stores concrete environments.

Examples:

- GitHub repository;
- VPS;
- development PC;
- hardware device.

Relations:

Project → Workspace

---

## WorkItem

Stores units of work.

Sources may include:

- GitHub;
- local tasks;
- manual input;
- external systems.

---

## Event

The main historical record.

Stores:

- id;
- project reference;
- timestamp;
- event type;
- source;
- payload.

Events are append-only.

---

## Decision

Stores accepted conclusions.

Contains:

- statement;
- reasoning;
- source;
- evidence references;
- status.

---

## Evidence

Stores supporting materials.

Examples:

- commit SHA;
- file;
- log;
- screenshot;
- conversation extract.

---

## ArchiveItem

Stores raw source materials.

Examples:

- exported conversations;
- raw logs;
- external documents.

Archive is not generated from structured memory.

Structured memory may be rebuilt from Archive.

---

## Conversation

Stores conversation metadata.

Supports:

- source tracking;
- chat branches;
- links to archived content.

---

## Snapshot

Stores a point-in-time project state.

Purpose:

- fast context restoration;
- handoff between sessions;
- recovery after interruptions.

---

# Preliminary relationships

```
Project
 |
 +-- Workspace
 +-- WorkItem
 +-- Event
 +-- Decision
 |       |
 |       +-- Evidence
 |
 +-- Snapshot

Conversation
 |
 +-- ArchiveItem
 +-- Decision
 +-- Evidence
```

---

# MVP storage scope

Required:

- Project;
- Workspace;
- Event;
- Decision;
- Evidence;
- ArchiveItem;
- Snapshot.

Deferred:

- distributed synchronization;
- complex indexing;
- autonomous workflow storage.
