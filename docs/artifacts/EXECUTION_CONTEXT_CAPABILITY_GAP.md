# Artifact: Execution Context Capability Gap

## Purpose

This artifact records a real architectural failure mode discovered during Companion design.

The purpose is to ensure that restored memory is not confused with restored execution capability.

---

# Problem

A session can successfully restore project memory:

```
Memory restored
```

while execution capabilities are missing:

```
Capabilities lost
```

Without explicit detection, the system may continue as if actions are available when they are not.

---

# Example

```yaml
execution_context:
  repository:
    name: genrudko/Plugins_AD5X

  context:
    handoff_available: true

  capabilities:
    github_read: false
    github_write: false
    workspace: false

  required:
    github_read: true
    github_write: true
```

---

# Expected Companion behaviour

During context restoration Companion should compare:

- required capabilities;
- currently available capabilities;
- last verification state.

If requirements are not satisfied, Companion should explicitly report:

```
Context restored.
Execution capabilities unavailable.
Required actions cannot be performed until access is restored.
```

---

# Architectural lesson

A valid handoff requires two independent restorations:

```
Project Memory
+
Execution Context
```

Memory continuity without capability continuity is incomplete.
