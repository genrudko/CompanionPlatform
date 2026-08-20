# Companion Platform — Domain Model

## Purpose

This document defines the core domain entities of Companion Platform.

The goal is to describe the objects that the system stores and manages independently from any specific interface, LLM provider, or external service.

Companion Core is built around these concepts.

---

# Design principles

## State belongs to Companion Core

Chat sessions, UI clients and AI models are temporary interfaces.

Persistent engineering state belongs to Companion Core.

---

## Context is a first-class object

The system must preserve:

- what happened;
- why it happened;
- what proves it;
- what depends on it.

---

## Evidence over assumptions

Important state changes should be connected with evidence.

Examples:

- git commit;
- file;
- command output;
- test result;
- screenshot;
- conversation extract.

---

# Core entities

---

# Project

## Definition

A Project represents an engineering or operational domain managed by Companion.

Examples:

- CompanionPlatform;
- EOD;
- EEP;
- AD5X;
- XSDE.

## Contains

- identity;
- workspaces;
- work items;
- decisions;
- events;
- snapshots.

---

# Workspace

## Definition

A Workspace represents a concrete environment where project artifacts exist.

Examples:

- GitHub repository;
- development PC;
- VPS;
- X96 box;
- physical hardware.

## Purpose

Workspace separates a logical project from its physical execution or storage location.

---

# WorkItem

## Definition

A WorkItem represents a unit of work.

Companion does not replace external task systems.

A WorkItem can originate from different sources:

- GitHub issue;
- local task;
- manual request;
- external system.

## Contains

- title;
- status;
- source;
- related decisions;
- evidence;
- artifacts.

---

# Source

## Definition

Source describes where an entity or event originated.

Possible sources:

- local;
- GitHub;
- conversation;
- manual input;
- agent;
- external system.

---

# Event

## Definition

An Event represents something that happened.

Examples:

- commit created;
- file changed;
- test completed;
- service restarted;
- decision accepted.

Events are immutable historical facts.

---

# Decision

## Definition

A Decision represents an accepted engineering or operational choice.

Contains:

- statement;
- reasoning;
- date;
- author;
- source;
- evidence.

---

# Evidence

## Definition

Evidence supports or proves a state, decision or event.

Examples:

- commit SHA;
- diff;
- log;
- test result;
- document;
- screenshot;
- conversation extract.

---

# Snapshot

## Definition

A Snapshot represents the known state of a project at a specific point in time.

Purpose:

Fast context restoration.

---

# Conversation

## Definition

A Conversation represents an interaction source.

Examples:

- ChatGPT conversation;
- exported chat;
- technical discussion.

A conversation is not the source of truth.

It is a source from which decisions, evidence, events and context can be extracted.

---

# Agent

## Definition

An Agent is an entity capable of analysis or actions.

Examples:

- OpenRouter summarizer;
- Git watcher;
- Linux executor;
- MCP adapter.

Agents operate under permissions.

---

# Tool

## Definition

A Tool is a capability available to a user or agent.

Examples:

- read_file;
- git_diff;
- run_command;
- execute_test.

---

# Permission

## Definition

Permission defines allowed operations.

Examples:

Allowed:

- read repository;
- collect logs;
- run tests.

Restricted:

- merge code;
- delete data;
- modify production systems.

---

# Initial Core MVP scope

Required:

- Project;
- Workspace;
- WorkItem;
- Event;
- Decision;
- Evidence;
- Snapshot.

Deferred:

- advanced agents;
- autonomous workflows;
- UI-specific entities.
