# Execution Context Handoff Failure Case

## Purpose

This document captures a real architectural failure scenario discovered during Companion design.

The problem:

> Project memory was restored, but execution capabilities were not.

A restored context without verified capabilities can create a false impression that work can continue.

---

# Failure scenario

Expected:

```
Memory restored
+
Capabilities restored
=
Ready to continue
```

Actual failure mode:

```
Memory restored
+
Capabilities lost
=
System incorrectly assumes continuation is possible
```

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

The system knows the project history but does not have the required tools to continue execution.

---

# Required behaviour

Before restoring a working session, Companion must validate:

1. Project memory availability.
2. Execution context availability.
3. Required capability availability.
4. Tool bindings validity.

If capabilities are missing, Companion must explicitly report:

```
Context restored.
Execution unavailable.
Missing capabilities:
- github_read
- github_write
```

---

# Architectural rule

A successful handoff requires:

```
Project Memory
+
Execution Context
+
Capability Validation
```

Memory alone is not a complete working context.
