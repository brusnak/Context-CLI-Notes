#CTX — Context Management CLI

CTX A lightweight, filesystem-aware command-line context manager for tracking project metadata, tasks, notes, and status on a per-directory basis.
CTX is designed to keep your working context close to the code with:
Zero background daemons
Plain JSON storage
Fast shell access
Optional shell prompt integration
It works especially well for developers who jump between many repositories, environments, or long-running projects and want instant situational awareness.

**Features:**
 - Per-directory context tracking
 - Unique tags for fast lookup and navigation
 - Task management (open, toggle, archive)
 - Notes, brief, and full descriptions
 - Project status (active, paused, archived)
 - Recent activity tracking
 - Global context listing
 - Shell integration
 - Prompt status indicator
 - Prompt tag display
 - jump command for instant directory navigation
 - Interactive configuration
 - Prompt-safe output (ANSI-aware)
 
**Philosophy:**
 
 CTX is intentionally:
 - Local – Context is tied to directories, not Git repos or cloud services
 - Transparent – All data is readable JSON
 - Low-friction – No mandatory workflows
 - Shell-native – Designed to live inside your prompt, not replace it

**Installation:**

Place the script somewhere in your $PATH, for example:

```bash
~/bin/ctx
```

Make it executable:

```bash
chmod +x ~/bin/ctx
```

Run Setup (Optional, but recommended for prompt integration and jump command):

```bash
ctx setup
```

**Data Storage:**

CTX stores all context data under:

```text
~/.context_data/
```

Each directory context is stored as a single JSON file whose filename is derived from the absolute path.
Configuration is stored in:

```text
~/.ctxconfig
```

**Core Concepts**
 - Context
A context represents metadata associated with a directory:

 - Project name
 - Tag (unique identifier)
 - Status
 - Tasks
 - Notes
 - Descriptions
 - History

Contexts are directory-specific, but tags allow global lookup.

**Tags:**
 - Each context has one primary tag
 - Tags are globally searchable
 - CTX prevents accidental duplicates (with override confirmation)
 - Tags are used for:
 - Jumping between directories
 - Prompt display
 - Global listings
 
**Status:**
Each context has a status:

active
paused
archived

Status affects:
Prompt indicator symbol
Sorting in global views
Visual color coding
Commands Overview
Context Lifecycle

Initialize a new context in the current directory:

```bash
ctx add
```

View a context in the current directory or globally with view <tag>:

```bash
ctx view
ctx view <tag>
```

Interactive editor for tasks, notes, status, descriptions, and deletion:

```bash
ctx edit
```

List all contexts, sorted by status and tag.

```bash
ctx global
```

Show the 5 most recently updated contexts:

```bash
ctx recent
```

**Task Management:**

Add a task:

```bash
ctx task add "Task description"
```
Toggle a task:

```bash
ctx task toggle <task #>
```

Archive a task:

```bash
ctx task done <task #>
```

List tasks:

```bash
ctx task list
```

Completed tasks can be archived manually or automatically (configurable).

**Tags:**

Print the current context tag (prompt-safe).

```bash
ctx tags
```

Change the context's tag:

```bash
ctx tag set <new-tag>
```

Print all tags (used for shell completion):

```bash
ctx list-tags-only
```

**Status:**

ctx status command:

```bash
ctx status set <active|paused|archived>
```

**Navigation:**
Print the directory path for a tag:

```bash
ctx path <tag>
```

Jump (cd) directly to the directory for a context tag
(installed via ctx setup):

```bash
jump <tag>
```

**Shell Integration:**

CTX integrates with your shell in two ways:

1. Prompt Indicators (PS1)

CTX provides prompt-safe helpers:

ctx check   # status indicator
ctx tags    # tag display


Example output:

[+] <api>
[#] <docs>
[!] <legacy>


Where:
+ = active

\# = paused

! = archived


**Automatic Setup:**

Running:

```bash
ctx setup
```

Appends the following to ~/.bashrc:

Jump Function(ie. jump <tag>)

Simple Prompt Injection
PS1="\u@\h $(ctx check)$(ctx tags) $ "


Manual Prompt Integration (Recommended for Custom Prompts):

If you already use a custom prompt, do not rely on automatic injection.
Instead, append manually:

$(ctx check)$(ctx tags)


Example:

```
PS1="[\\u@\\h \\W] $(ctx check)$(ctx tags) $ "
```

**Configuration:**

Run:

```bash
ctx config
```

Settings include:

 - Detail level (brief, full, both)
 - Default status
 - Auto-archive completed tasks
 - Unicode icons
 - Colors
 - Date format
 - Editor
 - Max tasks displayed

Config file:

```
~/.ctxconfig
```

**Error Handling & Logging:**
Unexpected errors are logged to:

```
~/ctx_error.log
```

The CLI is resilient to corrupted or missing context files.



**Known Limitations:**
 - One primary tag per context
 - No background syncing
 - No native Zsh prompt injection
 - Prompt injection is Bash-focused
 - No concurrent editing protection
 - No encryption (data is plaintext JSON in users home directory)

**Use Cases:**
 - Tracking active development work
 - Long-running infrastructure projects
 - Consulting/client engagements
 - Homelab documentation
 - Learning projects
 
