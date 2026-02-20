# plane-so-cli

Claude Code skill to manage [Plane.so](https://plane.so) projects and work items from the terminal.

**Zero dependencies** — uses only Python 3.8+ stdlib.

## Install

```bash
claude skill install luiseduardoaugusto/plane-so-cli
```

## Setup

Set these environment variables:

```bash
export PLANE_API_KEY="your-api-key"
export PLANE_WORKSPACE="your-workspace-slug"
```

Get your API key from **Plane > Profile Settings > Personal Access Tokens**.

## What it does

- List projects, members, states, labels, cycles, and modules
- Create, update, assign, delete, and search issues (work items)
- Add and list comments on issues
- View your assigned issues across all projects
- Output as human-readable tables or raw JSON

## Commands

| Command | Description |
|---------|-------------|
| `plane-so-cli me` | Show current user |
| `plane-so-cli projects list` | List all active projects |
| `plane-so-cli members` | List workspace members |
| `plane-so-cli issues list -p PROJECT_ID` | List issues in a project |
| `plane-so-cli issues create -p PROJECT_ID --name "Task"` | Create an issue |
| `plane-so-cli issues update -p PROJECT_ID ISSUE_ID --priority high` | Update an issue |
| `plane-so-cli issues assign -p PROJECT_ID ISSUE_ID USER_ID` | Assign an issue |
| `plane-so-cli issues delete -p PROJECT_ID ISSUE_ID` | Delete an issue |
| `plane-so-cli issues search "query"` | Search across workspace |
| `plane-so-cli issues my` | Show my assigned issues |
| `plane-so-cli comments add -p PROJECT_ID -i ISSUE_ID "text"` | Add a comment |
| `plane-so-cli states -p PROJECT_ID` | List workflow states |
| `plane-so-cli labels -p PROJECT_ID` | List labels |
| `plane-so-cli cycles list -p PROJECT_ID` | List cycles |
| `plane-so-cli modules list -p PROJECT_ID` | List modules |

Use `-f json` on any command for raw JSON output.

## Typical workflow

```bash
plane-so-cli projects list                                          # find project ID
plane-so-cli members                                                # find member IDs
plane-so-cli states -p PROJECT_ID                                   # see available states
plane-so-cli issues create -p PROJECT_ID --name "Task" --assignee USER_ID
plane-so-cli comments add -p PROJECT_ID -i ISSUE_ID "Started working"
```

## License

MIT
