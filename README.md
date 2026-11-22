# pi-prompt-history-x

**English** · [简体中文](README.zh-CN.md)

Recall past pi prompts with ↑/↓ or search them with Ctrl+R. This fork also recalls skill invocations as `/skill:name args` and keeps slash prompts that were sent to the model.

[Install](#install) · [Keyboard shortcuts](#usage) · [Upstream change](https://github.com/ravshansbox/pi-prompt-history/pull/7)

## Install

This fork is not published to npm. Install it from source on GitHub:

```bash
pi install git:github.com/Fracizz/pi-prompt-history-x@v0.3.0
```

Leave off `@v0.3.0` to track the latest commit on `main` instead of the pinned release. Do not install it alongside `@ravshansbox/pi-prompt-history`; both bind Ctrl+R.

Add `-l` to install it in project settings. Open a new interactive pi session in a folder with previous sessions and press Ctrl+R to search those prompts.

## Usage

Pi loads the extension from `./index.ts`. When pi starts, it loads the user prompts from your previous sessions **in the current working directory** and seeds them into the editor's history. It only activates in interactive (TUI) mode.

- **Up / Down** — recall the previous / next prompt (when the cursor is at the top / bottom of the editor, exactly like bash/zsh)
- **Ctrl+R** — reverse search: an incremental, fuzzy picker over your past prompts. Type to filter, Up/Down to move, Tab to switch between current-folder and all-folder history, Enter to load the prompt into the editor, Esc to cancel. If the editor already contains text, Ctrl+R uses it as the initial search query.

### Behaviour

- **Scope:** Up/Down recall and the default Ctrl+R tab use sessions started in the current folder (via `SessionManager.list(cwd, sessionDir)`). Ctrl+R also has an **All folders** tab backed by `SessionManager.listAll()`, or by the custom session folder when pi uses one.
- **Filtering:** empty input and inline bash (`!`, `!!`) are skipped, matching shell history hygiene. Prompts starting with `/` that were sent to the model are kept; built-in and extension commands such as `/model` are never written to sessions, so they do not appear.
- **Skill commands:** an expanded skill block is recalled as the `/skill:name args` command that produced it, so picking it re-runs the skill with its current instructions.
- **De-duplication:** global — repeated prompts collapse to their most recent position.
- **Ordering:** chronological, so the first Up press recalls your newest prompt. Prompts that pi replays when you resume a session or move in the tree keep their place.
- **Limits:** each reverse search scope covers up to the 500 most recent unique prompts. Up/Down uses pi's built-in history ring, which keeps the most recent ~100 prompts plus anything you type during the session.
- New prompts you submit during the session are added to history immediately.

## Development

```bash
npm install
npm run check
```

## Upstream and licence

Forked from [Ravshan's pi-prompt-history](https://github.com/ravshansbox/pi-prompt-history) under the same [MIT licence](LICENSE). The skill and slash-prompt recall change is also [proposed upstream](https://github.com/ravshansbox/pi-prompt-history/pull/7). If it is merged, prefer the original package.
