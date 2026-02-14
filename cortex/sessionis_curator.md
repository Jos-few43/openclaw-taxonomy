# Cortex.SessionisCurator (Session Manager)

**Taxonomy:** `Cortex.SessionisCurator`
**Project:** CORTEX (Phase 1)
**Status:** Draft / Specification

## 1. Objective
To transition OpenClaw from a collection of isolated processes to a cohesive, aware ecosystem. The `SessionisCurator` acts as the "Lobbyist," greeting new sessions with a situational awareness report of all other active agents.

## 2. Core Functions

### A. The "State of the Union" (Status Unionis)
A generated summary of global state.
- **Input:** `sessions_list` + `sessions_history` (last 5 messages of each).
- **Process:**
  1. Filter out idle/sleeping sessions.
  2. Identify "Clusters of Intent" (e.g., "3 sessions working on coding", "1 research agent").
  3. Detect duplicates or opportunities for merge.
- **Output:** A concise Markdown block:
  ```markdown
  🌍 **Active Contexts:**
  - 🛠️ **Dev:** `coding-agent-1` is debugging `server.py`.
  - 🔬 **Research:** `deep-researcher` found 4 papers on "Project Supra".
  - 💤 **Idle:** 2 sessions (no activity > 1h).
  
  *Suggestion: You seem to be starting a dev task. Link to `coding-agent-1`?*
  ```

### B. The Greeter Hook (Salutator)
A mechanism to inject the *Status Unionis* into the start of a new Main Session.
- **Trigger:** `BOOTSTRAP.md` execution or `init` event.
- **Action:** Run the analysis and post it immediately as the first system event or assistant message.

### C. The Aggregator (Aggregatus)
A command to explicitly pull context.
- **Command:** `/sessions merge [id]` or `/summary`
- **Behavior:** Fetches the full context of a target session and summarizes it into the current one, effectively "joining" the effort without killing the other process.

## 3. Implementation Plan

### Phase 1: The Script (Scriptum)
Create `scripts/cortex/session_scanner.py`:
- Uses `sessions_list` tool logic (via API or CLI).
- Fetches history for active ones.
- Uses a cheap model (Gemini Flash/Haiku) to generate the 1-paragraph summary.

### Phase 2: The Hook (Uncus)
Modify `BOOTSTRAP.md` (or the `openclaw` startup config if accessible, otherwise user-space bootstrap) to run:
`python3 scripts/cortex/session_scanner.py --greet`

### Phase 3: The Manager Agent (Curator)
A persistent background agent that:
- Monitors `sessions_list` every 10m.
- Updates a shared `memory/active_state.json`.
- Kills "zombie" sessions (stuck/looping) after asking permission.

## 4. Dependencies
- Python 3.11+
- `llm` CLI or direct API access for the summary step.
- OpenClaw CLI (`openclaw sessions ...`).
