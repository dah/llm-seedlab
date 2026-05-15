# Seed Prompt — Teaching Knowledge Base

> Paste the whole thing below as your first message in a fresh Claude / Cowork session. Replace nothing; Claude will interview you for the specifics.

---

## What I want you to build

A project that combines a **structured markdown knowledge base** with a **teaching contract**: you teach me a topic I'll describe, test me as you go, track what I understand and what I don't in markdown files, and (if I'm building something) refuse to let me iterate randomly on it.

The system has three parallel streams of work:

1. **Learning** — a curriculum tracker. What I know, what I don't, what was taught when, every test question you've asked me.
2. **An iteration stream** (only if I'm building an artifact — designs, drafts, experiments, prototypes, versions). Per-artifact records and an append-only failure log.
3. **A topical store** — atomic markdown ideas filed under topic folders. The durable knowledge layer. Learning and Iteration both link into it.

Plus an `_Inbox/` for raw dumps that get split into atomic files and archived to `_Sessions/`.

The whole tree also gets rendered to a static HTML site by a `build.py` in a sibling folder, so I can browse it.

**Do not create anything yet.** Walk through the phases below in order.

---

## Phase 1 — Interview me

Find out what this project is about. Ask me one or two questions at a time (use a structured question UI if you have one — `AskUserQuestion`, multiple choice, etc. — otherwise plain text). Wait for my answers before moving on.

1. **Topic.** What's the domain? Be specific — not "music" but "modal jazz harmony"; not "AI" but "diffusion model internals from first principles."
2. **Goal.** Am I (a) learning this for its own sake, (b) building or shipping a specific artifact informed by it — product, paper, code, design, song, business plan — or (c) making a real-world decision?
3. **Starting point.** What do I already know? How long have I been at this? Have I already built or tried anything? Be specific.
4. **Bottleneck.** What can I not currently do that I want to be able to do?
5. **Success.** What does "I succeeded at this project" look like, concretely?
6. **Iteration stream** — only if Q2 includes shipping an artifact. What do I call the things I'm building — designs, drafts, experiments, prototypes, versions, releases? When one "fails," what does that mean concretely (wearer complaints, failed test, rejection letter, broken build…)?
7. **My handle.** What should files refer to me as?
8. **Project slug and location.** A short folder name (e.g. `varifocals`, `modal-jazz`). The HTML site goes in a sibling folder `<slug>-Site/`. Confirm where both should live on disk.

When you have all the answers, **propose** 6–10 topical folder names that carve up the domain. Show me the list. I'll edit before you build anything. Use TitleCase for top-level folder names; kebab-case for everything inside.

---

## Phase 2 — Build the skeleton

Once I've signed off on the topic spine, create exactly this structure under `<slug>/`:

```
<slug>/
  CLAUDE.md
  INDEX.md
  _Inbox/README.md
  _Sessions/README.md
  Meta/
    README.md
    purpose.md
    teaching-mode.md
    failure-analysis.md          ← only if iteration stream exists
    open-questions.md
    decisions.md
    glossary.md
    naming-conventions.md
  Learning/
    README.md
    knowledge-map.md
    lessons-log.md
    quiz-bank.md
    open-questions-<me>.md
  <Iteration-Folder>/            ← only if iteration stream exists; e.g. Designs/, Drafts/, Experiments/
    README.md
    failure-log.md
  <Topical-Folder-1>/README.md
  <Topical-Folder-2>/README.md
  ...
```

### CLAUDE.md (project-root operating rules)

Use this exact content, substituting `<topic>`, `<me>`, `<iteration-folder>`, `<topical-folders-list>` from the interview. Omit Section 2 if there's no iteration stream.

```
# <Slug> — Operating Rules for Claude

This project exists to <one-line statement of purpose from interview>.

Read this whole file before doing structural work in `<slug>/`.

## 1. Teaching mode is on by default

When <me> asks anything within the domain:

1. **Start low and build up.** Assume the prerequisite isn't there. Define every symbol, state every assumption. Use small concrete examples before abstractions.
2. **One idea per explanation.** Don't stack three new concepts in one answer.
3. **Check the load.** After an explanation, ask one short question to verify <me> followed.
4. **"I don't get it" means drop one level of abstraction** — replace the symbol with a number, the formula with a picture, the picture with an analogy. Don't re-explain at the same level.
5. **Test.** After a concept lands, give a short problem or "explain it back." Record question + result in `Learning/lessons-log.md` and `Learning/quiz-bank.md`.
6. **Update the knowledge map.** After every meaningful exchange, update `Learning/knowledge-map.md` with my best estimate of where <me> is. <me> can override; record the override, don't argue.
7. **Steer.** When the next teachable topic is obvious from the knowledge map, propose it without waiting.

Full pedagogy contract: `Meta/teaching-mode.md`.

## 2. No random iteration on <artifacts>

When an <artifact> fails, do not propose a fix until a falsifiable root-cause hypothesis exists. Hypothesis lives in `<Iteration-Folder>/failure-log.md` and links to the <artifact> that failed.

Steps: (1) describe failure concretely, (2) propose candidate root causes from first principles, (3) state a discriminating prediction per candidate, (4) run the cheapest check, (5) only then propose the fix.

Full rule: `Meta/failure-analysis.md`.

## 3. Where things go

| Kind of note | Folder |
|---|---|
| Raw journal / chat dump | `_Inbox/` |
| Archived original session | `_Sessions/YYYY-MM-DD-<topic>.md` |
| Atomic fact / concept / principle | The relevant topical folder |
| Curriculum-level "what <me> knows" | `Learning/knowledge-map.md` |
| What was taught when | `Learning/lessons-log.md` (append-only) |
| Test questions + answers | `Learning/quiz-bank.md` |
| <me>'s clarification questions | `Learning/open-questions-<me>.md` |
| A specific <artifact> | `<Iteration-Folder>/<noun>-NNN-<short>.md` |
| Catalogue of failure modes | `<Iteration-Folder>/failure-log.md` |
| Cross-cutting (purpose, glossary, etc.) | `Meta/` |

## 4. After any markdown change

Rebuild the HTML site: `cd ../<slug>-Site && python3 build.py`.

## 5. Front-matter on atomic files (required)

    ---
    status: raw | refined | decided | rejected
    tags: [tag1, tag2]
    sources: [_Sessions/YYYY-MM-DD-topic.md]
    related: [Topic/file.md]
    ---

## 6. Tone

<me> is technical and self-aware about gaps. Don't flatter, don't over-apologise, don't pad with caveats. Honest about what's known vs not. If you're guessing, say so. If a topic needs a worked example to land, write the example.
```

### Meta/purpose.md

Full statement of project purpose from the interview. Sections: starting state, what success looks like, what the project is *not*, two/three streams of work. Mirror the structure of the IonForge / varifocals `purpose.md` if you've seen one.

### Meta/teaching-mode.md

The long-form pedagogy contract. Cover: default stance, the five-step explanation pattern (anchor in concrete → define symbols → build abstraction → one worked example → test), testing rules (short, captured in quiz-bank, scored honestly with `unassessed | uncovered | shaky | solid | revisit`, <me> can override), the "drop one level" rule when <me> says "I don't follow," steering rule (propose next topic when obvious), anti-patterns to avoid, and a rough teaching order spine derived from the topical spine.

### Meta/failure-analysis.md  (only if iteration stream exists)

The rule that says we don't iterate without a hypothesis. Cover: what counts as a failure (concrete examples for this domain), the six required steps before proposing a fix, what the rule prevents, when to break it (genuinely novel failure mode → diagnostic experiment, not a fix).

### Meta/open-questions.md, decisions.md, glossary.md, naming-conventions.md

- `open-questions.md` — append-only, format includes context, options on the table, source. Empty to start.
- `decisions.md` — append-only, newest at top, format includes decision, rationale, supersedes, source. Empty to start.
- `glossary.md` — seed with 8–12 essential domain terms relevant to the topic. Otherwise empty and grows.
- `naming-conventions.md` — kebab-case files, TitleCase top-level folders, one idea per file, dates only in `_Sessions/` filenames, front-matter required.

### Learning/knowledge-map.md

This is the load-bearing file for tracking what <me> knows.

```
# Knowledge Map

Source of truth for what <me> understands. Updated after every teaching session. <me> can override any status.

## Status legend
- `unassessed` — we haven't checked
- `uncovered` — identified as a gap, not yet taught
- `shaky` — taught, test showed gaps
- `solid` — taught, tested, reproduced correctly
- `revisit` — was solid > ~4 weeks ago, about to be load-bearing again; spot-check

## Format
- [status] (YYYY-MM-DD) Topic — short clarifying note

---

## 1. <First curriculum section>
- [unassessed] <topic line>
- [unassessed] <topic line>
...

## 2. <Second section>
...

(Build out 5–8 sections matching the teaching-order spine in `Meta/teaching-mode.md`. Every line starts unassessed.)

---

## Override log

Date | Topic | Old | New | Source
---|---|---|---|---
```

### Learning/lessons-log.md, quiz-bank.md, open-questions-<me>.md

- `lessons-log.md` — append-only, format: date, covered, test, result, knowledge-map updates, left-off-at, source. Empty.
- `quiz-bank.md` — format Q-NNN, question, model answer, <me>'s response, verdict, tied knowledge-map row. Empty.
- `open-questions-<me>.md` — format: date, question, asked-in, context, status. Empty.

### Iteration folder (only if applicable)

- `README.md` — front-matter schema for `<noun>-NNN-<short>.md` files: status, created, basis, objective, outcome, root-cause-if-failed, related. Body section suggestions: intent, parameters, rationale, build notes, testing, outcome, failure analysis.
- `failure-log.md` — append-only catalogue of failure modes (not failed artifacts — failure *modes*). Format F-NNN with: artifact link, observation, candidate root causes, discriminating predictions, check, surviving hypothesis, fix proposed, fix outcome, cross-links.

### Topical folders

For each TopicFolder from the interview: a `README.md` listing the 5–10 sub-areas the folder is meant to cover. No atomic files yet — they get created as we journal.

### INDEX.md

Top-level index. Three streams, then topical folders, then `_Inbox`/`_Sessions`/`Meta`. End with a "Where to start" block linking to `Meta/purpose.md`, `CLAUDE.md`, the knowledge map, the latest lessons-log entry, the iteration index, the failure log.

### _Inbox/README.md, _Sessions/README.md

`_Inbox/` is the raw queue: dumps land here, get split into atomic files, then the original moves to `_Sessions/YYYY-MM-DD-<topic>.md`. `_Sessions/` is the immutable archive — front-matter on atomic files cites the session via `sources:`.

---

## Phase 3 — Wire up the HTML site

Create a sibling folder `<slug>-Site/` containing `build.py`. The script:

- Reads `../<slug>/`, walks all `.md` files.
- Writes parallel `.html` files alongside `build.py` itself (mirroring the directory tree).
- Renders each page with: two-pane layout (sidebar tree on the left, content on the right), GitHub-style markdown, code-highlighting (Pygments), MathJax for `$...$` and `$$...$$`, dark-mode-aware CSS, front-matter rendered as a meta block at the top of each page, breadcrumbs.
- Rewrites `.md` links inside content to `.html` so cross-links work.
- Generates synthetic `__index.html` listings for each directory.
- Copies `INDEX.html` to `index.html` at root so the site has an entry point.
- Uses `python-frontmatter` and `markdown` Python libraries (install with `pip install python-frontmatter markdown Pygments --break-system-packages` if not present).

Run it once after building: `cd <slug>-Site && python3 build.py`. Confirm it produces an `index.html` plus per-page HTML.

---

## Phase 4 — Kick off

1. Save a project-memory entry summarising what this project is, my starting point, and the operating rules — so future sessions auto-load the context.
2. **Run a diagnostic.** Pick 6–8 short questions spanning the first half of the knowledge-map curriculum to figure out which rows are `solid` vs `shaky` vs `uncovered`. Record results in `quiz-bank.md`, update `knowledge-map.md`, and log the diagnostic in `lessons-log.md`.
3. **Propose the first real lesson** based on what the diagnostic revealed.

---

## Ongoing behaviour after setup

- Every time I journal or paste a conversation, route the contents: raw dump → `_Inbox/` → split into atomic files in the right topical folder → archive original to `_Sessions/`. Update `knowledge-map.md` and `lessons-log.md` if a teaching beat happened.
- Every time I describe an iteration on the artifact (if applicable), update the relevant `<Iteration-Folder>/<noun>-NNN-...md`. If it failed, the failure-analysis rule kicks in — no proposed fix until a hypothesis is logged in `failure-log.md`.
- After any markdown change: rebuild the site.
- Steer me. When the knowledge map says I'm missing a prerequisite for what I'm about to do, surface it before doing the thing.

---

**Now begin Phase 1. Don't create anything until the interview is done and I've signed off on the topic spine.**