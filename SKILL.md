---
name: plane-so-cli
description: "Manage Plane.so projects and work items using a clean, zero-dependency Python CLI. List projects, create/update/assign issues, add comments, search workspace."
metadata: {"moltbot":{"requires":{"env":["PLANE_API_KEY","PLANE_WORKSPACE"]},"primaryEnv":"PLANE_API_KEY","emoji":"✈️"}}
---

# Plane.so CLI Skill

Interact with [Plane.so](https://plane.so) project management via a clean, auditable Python CLI.

**Zero dependencies** — uses only Python 3.8+ stdlib.

## IMPORTANT: Environment Setup

**Before every command, source the environment file:**

```bash
source /workspace/.env && plane-so-cli <command>
```

## Setup

Create `/workspace/.env` with:

```bash
export PLANE_API_KEY="your-api-key"
export PLANE_WORKSPACE="your-workspace-slug"
```

Get your API key: **Plane → Profile Settings → Personal Access Tokens**

## Commands

### Me
```bash
plane-so-cli me                    # Show current user
```

### Projects
```bash
plane-so-cli projects list         # List all projects (active only)
```

### Members
```bash
plane-so-cli members               # List workspace members (for assignments)
```

### Issues (Work Items)
```bash
# List issues in a project
plane-so-cli issues list -p PROJECT_ID
plane-so-cli issues list -p PROJECT_ID --state STATE_ID
plane-so-cli issues list -p PROJECT_ID --priority high
plane-so-cli issues list -p PROJECT_ID --assignee USER_ID

# Get issue details
plane-so-cli issues get -p PROJECT_ID ISSUE_ID

# Create issue
plane-so-cli issues create -p PROJECT_ID --name "Fix bug" --priority high
plane-so-cli issues create -p PROJECT_ID --name "Task" --assignee USER_ID

# Update issue
plane-so-cli issues update -p PROJECT_ID ISSUE_ID --state STATE_ID
plane-so-cli issues update -p PROJECT_ID ISSUE_ID --priority medium

# Assign issue
plane-so-cli issues assign -p PROJECT_ID ISSUE_ID USER_ID_1 USER_ID_2

# Delete issue
plane-so-cli issues delete -p PROJECT_ID ISSUE_ID

# Search across workspace
plane-so-cli issues search "login bug"

# My issues (assigned to me)
plane-so-cli issues my
```

### Comments
```bash
plane-so-cli comments list -p PROJECT_ID -i ISSUE_ID
plane-so-cli comments add -p PROJECT_ID -i ISSUE_ID "Comment text"
```

### States & Labels
```bash
plane-so-cli states -p PROJECT_ID     # List workflow states
plane-so-cli labels -p PROJECT_ID     # List labels
```

### Cycles
```bash
plane-so-cli cycles list -p PROJECT_ID
plane-so-cli cycles get -p PROJECT_ID CYCLE_ID
```

### Modules
```bash
plane-so-cli modules list -p PROJECT_ID
plane-so-cli modules get -p PROJECT_ID MODULE_ID
```

## Output Formats

Default is human-readable table. Use `-f json` for raw JSON:

```bash
plane-so-cli projects list -f json
plane-so-cli issues list -p PROJECT_ID -f json
```

## Typical Workflow

1. `plane-so-cli projects list` — find project ID
2. `plane-so-cli members` — find member IDs for assignment
3. `plane-so-cli states -p PROJECT_ID` — see available states
4. `plane-so-cli issues create -p PROJECT_ID --name "Task" --assignee USER_ID`
5. `plane-so-cli comments add -p PROJECT_ID -i ISSUE_ID "Started working"`
