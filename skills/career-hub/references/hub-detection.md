# Hub Detection

How sub-skills decide whether the current working directory is a career hub, and how they confirm before acting.

## Signals of a compliant hub

A directory is a hub if all of these are true:

1. `PRINCIPLES.md` exists at the directory root.
2. All seven category directories exist: `a.foundations/`, `b.history/`, `c.projects/`, `d.capabilities/`, `e.artefacts/`, `f.pipeline/`, `g.backlog/`.
3. `README.md` exists at the directory root.

A directory with some but not all of these is **malformed** — refuse to proceed and surface the gap.

## Sub-skill confirmation behaviour

All three sub-skills (`init`, `build`, `publish`) confirm the hub location with the user on invocation, before taking any write action.

### For `init`

Refuses if the current directory already looks like a hub (any of the three signals present).

Refuses if the current directory is non-empty and does not look like a fresh scaffold target (contains files that are not `.gitignore`, `README.md`, or a single non-hub placeholder).

Confirms with:
```
Create a career hub at <cwd>? This will create approximately 40 files
(seven category directories, PRINCIPLES.md, README.md, templates).
Proceed? (y/n)
```

Proceeds only on explicit `y`.

### For `build` and `publish`

Requires all three signals present. If any signal is missing, refuse with a message identifying the gap and suggesting `init`.

Confirms with:
```
Hub detected at <cwd>.
<summary of category stub counts, e.g. "12 roles, 8 projects, 6 capabilities, 3 open backlog items">
Proceed with <build|publish> <arg>? (y/n)
```

Proceeds only on explicit `y`.

## Why cwd-scoped, not config-based

We deliberately do not use a `~/.career-hub/config.yaml` pointer. Rationale:

- Keeps per-machine state out of home directory.
- Matches the existing `cv-opti` pattern (cwd-scoped).
- A user with multiple hubs simply `cd`s to the right one.
- Explicit confirmation on every invocation catches mistakes early.

## Multi-hub situations

A user may maintain more than one hub (personal vs client-facing, for example). Each hub is independent. Sub-skills operate on whichever hub is at `cwd` when invoked.
