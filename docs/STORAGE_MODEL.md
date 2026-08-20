# Companion Platform — Storage Model

## Purpose

Этот документ определяет, как Companion Core хранит постоянную информацию.

Модель разделяет исторические факты, структурированные знания, текущее состояние и контекст выполнения.

---

# Storage principles

## Immutable history

Некоторые данные являются фактами и не должны перезаписываться.

Примеры:

- Events;
- Archive items;
- Evidence.

Исправления создают новые записи.

---

## Structured memory

Структурированные объекты представляют интерпретированные знания.

Примеры:

- Decisions;
- WorkItems;
- связи между сущностями.

---

## Operational state

Current State используется для ежедневной работы.

Он может быть восстановлен из истории и структурированной памяти.

---

# Initial storage backend

MVP target:

SQLite.

Причины:

- один переносимый файл;
- подходит для VPS, desktop и embedded-систем;
- простой backup и миграция.

---

# Core entities

## Project

Хранит идентичность проекта.

---

## Workspace

Хранит конкретные окружения.

Примеры:

- GitHub repository;
- VPS;
- development PC;
- hardware device.

---

## WorkItem

Хранит единицы работы из разных источников.

---

## Event

Основная историческая запись.

Хранит:

- идентификатор;
- проект;
- время;
- тип события;
- источник;
- данные.

Events являются append-only.

---

## Decision

Хранит принятые решения.

---

## Evidence

Хранит подтверждающие материалы.

---

## ArchiveItem

Хранит исходные материалы.

Structured Memory может быть перестроена из Archive.

---

## Conversation

Хранит метаданные разговоров.

Поддерживает:

- источники;
- ветвление чатов;
- связь с архивом.

---

## ExecutionContext

Хранит информацию о доступных возможностях выполнения действий.

ExecutionContext связывает состояние проекта с реальными возможностями среды.

Пример:

```yaml
execution_context:
  repository:
    name: genrudko/Plugins_AD5X

  access:
    github: true

  capabilities:
    read_files: true
    write_files: true
    run_tests: true

  last_verified:
    commit: 3b5dfc...
```

ExecutionContext должен учитывать не только права доступа, но и фактическую доступность исполнителей.

---

## Snapshot

Хранит состояние проекта в конкретный момент времени.

Snapshot включает:

- Project State;
- Execution Context;
- Tool Binding.

Назначение:

- быстрое восстановление контекста;
- handoff между сессиями;
- восстановление после перерывов.

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
 +-- ExecutionContext
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
- Snapshot;
- ExecutionContext.

Deferred:

- distributed synchronization;
- complex indexing;
- autonomous workflow storage.
