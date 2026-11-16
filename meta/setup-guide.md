---
tags: [meta]
---

# Setup guide — Anki, Obsidian, learning-log

Do the parts in order. Total time: about 60–90 minutes. Tick boxes as you go.

---

## Part 1 — Obsidian vault (the learning-log)

### 1.1 Put the vault in the right place
- [x] Unzip `learning-log` to the **Windows** side, e.g. `C:\Users\<you>\Documents\learning-log`.
  - Not inside WSL (`\\wsl$\...`): Obsidian runs on Windows and watches files poorly across that boundary. Keep code repos in WSL; keep this vault on Windows.
- [x] Obsidian → **Open folder as vault** → choose `learning-log`. Click **Trust author and enable plugins** if asked.

### 1.2 Core settings (Settings ⚙ bottom-left)
The zip already includes these, so just **check** they took:
- [x] **Files and links**
  - Default location for new notes: *In the folder specified below* → `notes/inbox`
  - Default location for new attachments: `attachments`
  - **Use [[Wikilinks]]: OFF** (normal Markdown links render on GitHub, since this repo is public)
  - New link format: *Relative path to file*
  - Automatically update internal links: ON
- [x] **Core plugins** — turn ON: *Daily notes*, *Templates*, *Backlinks*, *Outline*, *Bookmarks*, *Properties view*, *Command palette*, *File recovery*.
- [x] **Templates** → Template folder location: `templates`
- [x] **Daily notes** (used here as *weekly* notes):
  - Date format: `gggg-[W]ww`
  - New file location: `weekly`
  - Template file location: `templates/Weekly log`
  - Open daily note on startup: ON (optional — opens this week's log every time)

> **Check the week numbering:** the preview under Date format should show **2026-W47** for this week (15–21 Nov = plan Week 1). Weeks run **Sunday → Saturday**, matching your plan. If on Sun 22 Nov it opens W47 instead of **W48**, your app language uses Monday weeks — change the format to `GGGG-[W]WW` and just log Sundays in the next week's file.

### 1.3 Hotkeys (Settings → Hotkeys)
- [x] *Daily notes: Open today's daily note* → `Ctrl+Alt+W` (= "open this week's log")
- [x] *Templates: Insert template* → `Alt+T`
- [ ] *Git: Commit-and-sync* → `Ctrl+Alt+S` (after Part 1.5)

### 1.4 Create this week's log
- [x] Press `Ctrl+Alt+W` → `weekly/2026-W47.md` appears, pre-filled. Fill *Plan week: 1* and today's 3 lines.

### 1.5 Push it to GitHub (so it can be pinned on your profile)
1. [x] Install **Git for Windows** if `git --version` doesn't work in PowerShell. (The Obsidian Git plugin uses Windows Git, **not** the Git inside WSL.) Keep "Git Credential Manager" ticked in the installer.
2. [x] On GitHub: **New repository** → name `learning-log` → **Public** → *don't* add README/.gitignore (the vault already has them).
3. [ ] In PowerShell or Git Bash, inside the vault folder:
   ```bash
   git init -b main
   git add .
   git commit -m "Start learning log"
   git remote add origin https://github.com/<your-username>/learning-log.git
   git push -u origin main
   ```
   First push opens a browser window to sign in — that's Git Credential Manager.
4. [ ] Obsidian → Settings → **Community plugins** → *Turn on community plugins* → **Browse** → install **Git** (by Vinzent, formerly "Obsidian Git") → Enable.
5. [ ] Git plugin settings:
   - Auto commit-and-sync interval: `0` (you'll sync by hand at wrap-up — cleaner history), **or** `60` if you'd rather not think about it
   - Pull on startup: ON
   - Commit message: `log: {{date}}`
6. [ ] Daily wrap-up habit: write your 3 lines → `Ctrl+Alt+S`.

**Privacy:** anything in `private/` is git-ignored (job applications, LinkedIn drafts, salary notes). Everything else is public — no personal data, no secrets.

### 1.6 Optional plugins (skip for now if you like)
- **WakaTime** — counts note-writing time in your weekly WakaTime totals. Use the same API key as VS Code/Eclipse.
- Nothing else is needed. Avoid plugin rabbit holes in Week 1.

### 1.7 How the folders are used
| Where | What goes there | When |
|---|---|---|
| `weekly/` | 3-line daily entry, practice tally, Saturday review | Daily wrap-up (5 min), Saturday review (30 min) |
| `notes/<deck>/` | Concept notes in your own words (template: *Concept note*) — folders match Anki decks | When something is worth more than one card |
| `notes/inbox/` | Quick captures; sort into a deck folder on Sunday | Any time |
| `bugs/` | One note per bug that cost you >15 min (template: *Bug note*) | Right after fixing it |
| `prompts.md` | Your AI prompt templates + rules | Before any AI use |
| `private/` | Not pushed | — |

**Flow:** learn → make 1–3 Anki cards in the wrap-up → if it needed explaining, a concept note → if it was a bug, a bug note (→ one "Bug" card).

---

## Part 2 — Anki

### 2.1 Check version and sync
- [ ] **Help → About**: needs **23.10 or newer** for built-in FSRS. Update from apps.ankiweb.net if older.
- [ ] Create an **AnkiWeb** account → click **Sync** in Anki. Install **AnkiDroid** (Android, free) or **AnkiMobile** (iOS, paid) and sign in — handy for reviews on the bus.
- [ ] **Tools → Preferences**:
  - *Review* → Next day starts at: `4` hours past midnight (default is fine)
  - *Syncing* → Automatically sync on profile open/close: ON

### 2.2 Create the decks
Create Deck (bottom of main screen) — use `::` to make subdecks under one parent so one click reviews everything:
- [ ] `Dev::Java & Spring`
- [ ] `Dev::Web`
- [ ] `Dev::Testing`
- [ ] `Dev::Data & SQL`
- [ ] `Dev::Tools`
- [ ] `Dev::DSA`
- [ ] `Dev::Interview`

Every day you click **Dev**, not the subdecks.

### 2.3 One preset for all decks (gear next to **Dev** → Options)
- [ ] Top-right dropdown → **Rename** preset to `Dev`
- [ ] **Daily limits**: New cards/day `10` · Maximum reviews/day `150` (≈15 min once the deck matures; lower it if reviews spill over)
- [ ] **New cards**: Learning steps `1m 10m` (default) · **Lapses**: Relearning steps `10m` — keep all steps **under 1 day** with FSRS
- [ ] **FSRS** (near the bottom): toggle **ON** · Desired retention `0.90`
- [ ] **Display order**: leave defaults for now
- [ ] Save with the arrow next to Save → **Save to All Subdecks**

**Later (around mid-December, after a few hundred reviews):** come back here and click **Optimize** under FSRS parameters. Repeat about once a month.

### 2.4 Card formatting for code (once)
- [ ] **Tools → Manage Note Types → Basic → Cards… → Styling**, add at the bottom:
  ```css
  pre, code { font-family: Consolas, "Cascadia Code", monospace; font-size: 0.9em; }
  pre { text-align: left; background: #f4f4f4; padding: 8px; border-radius: 6px; overflow-x: auto; }
  .nightMode pre { background: #2b2b2b; }
  ```
- [ ] Do the same for **Cloze**.
- To add code on a card: in the editor press `Ctrl+Shift+X` (HTML editor) and wrap code in `<pre><code> … </code></pre>`.

### 2.5 Add a "Bug" note type
- [ ] **Tools → Manage Note Types → Add → Clone: Basic** → name `Bug`
- [ ] **Fields…** → rename/add so fields are: `Symptom`, `Code`, `Cause`, `Fix`
- [ ] **Cards…** → Front template:
  ```
  <b>Symptom:</b> {{Symptom}}
  {{#Code}}<pre><code>{{Code}}</code></pre>{{/Code}}
  <br>What's the cause, and the fix?
  ```
  Back template:
  ```
  {{FrontSide}}<hr id=answer>
  <b>Cause:</b> {{Cause}}<br><b>Fix:</b> {{Fix}}
  ```
  Paste the same CSS into Styling.

### 2.6 Which note type for what
| Card | Note type | Example |
|---|---|---|
| Syntax | **Cloze** | `record Point(int x, int y) {}` → hide `record` |
| Concept | Basic | "What problem do sealed classes solve?" |
| Own bug | **Bug** | Symptom → cause → fix |
| Big-O | Basic | "Time complexity of `HashMap.get` (average)?" |
| Interview | Basic | Question → 3-bullet answer outline (not a script) |

**Tags:** add `w01`, `w02` … plus the source (`devjava`, `odin`, `exercism`). Lets you find "everything from Week 1".

**Card rules:** one fact per card · your own words · you write them (no AI-written cards) · if you can't answer it in ~10 seconds, split it.

### 2.7 Sunday clean-up (10 min)
- [ ] **Browse** → search `deck:Dev tag:leech` → rewrite or split those cards, then unsuspend
- [ ] Search `deck:Dev flag:1` → fix cards you flagged red during the week (`Ctrl+1` while reviewing)
- [ ] Sort any `notes/inbox` notes into deck folders in Obsidian

---

## Part 3 — Other Week 1 setup

- [x] **WakaTime**: account → install plugin in **VS Code** and **Eclipse** (and optionally Obsidian) with the same API key. Your Saturday review depends on it.
- [x] **Exercism**: sign up → join the **Java** track → install the Exercism CLI and run `exercism configure --token=<token>` (token is on your Exercism settings page). Install a JDK (21 or 25) in the environment you'll code in.
- [x] **Codewars**: account, choose JavaScript, start at 8 kyu.
- [ ] **Khan Academy**: account; add the maths course you're starting with and try its **Course challenge** to test out of what you know.
- [ ] **Browser bookmarks folder** "Study": The Odin Project, dev.java, Exercism, Codewars, Khan Academy, Microsoft Learn (AI-901), WakaTime dashboard, AnkiWeb.

---

## The daily loop (once setup is done)
1. **15 min** — Anki: click **Dev**, review everything due.
2. **Main block** — Odin / dev.java / plan topic.
3. **30 min** — practice (Exercism Java, Codewars JS). AI off.
4. **5 min wrap-up** — `Ctrl+Alt+W` → 3 lines · add 1–3 Anki cards · `Ctrl+Alt+S` to push.
