SEED-PROMPT-SYSTEM-BUILDER
==========================

A single seed prompt that guides an AI agent through building a customisable knowledge-base system from scratch.

The prompt is intended to be pasted as the first message in a fresh AI-agent session. The agent interviews the user, proposes a project structure, waits for approval, and then creates a structured Markdown knowledge base plus a Python-generated static HTML site.

This is not just a passive writing prompt. It is a project bootstrap prompt: it asks an agent to create folders, create Markdown files, maintain operating rules, track learning progress, and create a Python program named `build.py` to render the knowledge base as a browsable website.

Critical Installation Warning
-----------------------------

Use a new, empty directory.

Do not install this into a folder that already contains documents, notes, drafts, source files, archives, or anything else you care about.

The prompt is designed to create and manage an entire system of files. That system includes a project root, operating rules, an inbox, session archives, metadata files, learning logs, quiz records, topical folders, optional iteration records, and a sibling static-site folder. If you aim it at a folder that already contains material, the generated system can become mixed with your existing files in a way that is annoying to untangle.

Create the system first. Copy documents into it later.

A good workflow is:

1. Create a new empty parent directory.
2. Start a fresh AI-agent session.
3. Paste in `SEED-PROMPT-SYSTEM-BUILDER.md`.
4. Complete the interview.
5. Approve the proposed topic structure.
6. Let the agent create the project.
7. Copy existing documents into `_Inbox/` only after the system exists.
8. Ask the agent to process, split, file, summarise, or link those documents according to the system rules.

Think of it a little like the Genesis Torpedo from Star Trek: powerful if deployed into empty space, but not something to fire into an existing world you care about.

Do Not Install Inside a Software Project
----------------------------------------

Do not install this system inside the root of an active software repository.

Do not install it inside a software project that you expect a coding agent to work on directly.

This prompt creates a knowledge-management and teaching layer with its own ongoing overhead: Markdown routing, lesson tracking, knowledge-map updates, quiz logging, optional failure-analysis logs, inbox/session archiving, and static-site rebuilds.

That is useful when the goal is to build a durable learning or research knowledge base. It is not useful when the main job is for a coding agent to edit, debug, refactor, test, or ship software. In that context, the extra rules and bookkeeping can make the coding agent less effective.

Instead:

1. Install this system in a separate empty directory.
2. Let the agent build the knowledge-base system there.
3. If a software repository is relevant, give the agent access to a separate clone of the repo after setup.
4. Let the knowledge-base system reference or analyse the clone without turning the codebase itself into the managed KB system.

Important Note Before Use
-------------------------

The enclosed prompt instructs the agent to create a Python program.

Specifically, it tells the agent to create a sibling site folder containing a `build.py` script. That script reads the generated Markdown knowledge base and renders it into a static HTML site.

Before using the prompt, make sure everyone involved is comfortable with the agent:

- creating directories and files;
- writing Markdown files;
- creating a Python program;
- installing or using Python dependencies where needed;
- running that Python program in the chosen workspace;
- maintaining logs, metadata, and generated site files over time.

The prompt itself tells the agent not to create anything immediately. It must first interview the user, propose the structure, and wait for sign-off before building. That approval step matters. Do not skip it.

What It Builds
--------------

The generated project is a structured Markdown knowledge-base system with three possible streams.

### 1. Learning

A curriculum tracker that records:

- what the user knows;
- what remains unclear;
- what has been taught;
- test questions asked by the agent;
- the user's answers;
- whether each topic is unassessed, uncovered, shaky, solid, or due for revisit.

The load-bearing files live under `Learning/`, especially:

- `knowledge-map.md`
- `lessons-log.md`
- `quiz-bank.md`
- `open-questions-<user>.md`

### 2. Iteration

An optional artifact-building stream for designs, drafts, experiments, prototypes, releases, or similar work.

If the user is building something, the prompt instructs the agent not to iterate randomly after failures. A failed artifact must first be described clearly, then tied to candidate root causes, discriminating predictions, and a cheap check. Only after that should the agent propose a fix.

This is intended to prevent "try random changes until something works" behaviour.

### 3. Topical Store

A durable collection of atomic Markdown notes organised into topic folders.

The topical store is the long-term knowledge layer. Learning logs and iteration records can link into it, but the topical notes are meant to be reusable and browsable on their own.

The system also includes:

- `_Inbox/` for raw dumps;
- `_Sessions/` for archived original sessions;
- `Meta/` for operating rules, purpose, teaching mode, decisions, glossary, and naming conventions;
- a sibling `<slug>-Site/` folder containing the static-site builder.

How the Prompt Works
--------------------

The prompt runs in four phases.

### Phase 1: Interview

The agent asks about the domain, goal, starting point, bottleneck, definition of success, project slug, file location, and any artifact or iteration workflow.

It then proposes a topic spine and waits for approval.

The prompt explicitly says not to create anything until the interview is complete and the user has signed off on the topic structure.

### Phase 2: Build the Skeleton

After approval, the agent creates the Markdown folder structure, including:

- `CLAUDE.md`
- `INDEX.md`
- `_Inbox/README.md`
- `_Sessions/README.md`
- `Meta/` files
- `Learning/` files
- optional iteration files
- topical folder README files

### Phase 3: Wire Up the HTML Site

The agent creates a sibling site folder containing `build.py`.

The script renders the Markdown tree into a static HTML site with:

- a two-pane layout;
- a sidebar tree;
- GitHub-style Markdown rendering;
- syntax highlighting;
- MathJax support;
- front-matter display;
- breadcrumbs;
- rewritten Markdown links;
- generated directory index pages.

### Phase 4: Kick Off

The agent records project context, runs an initial diagnostic quiz, updates the knowledge map, logs the results, and proposes the first real lesson.

Ongoing Behaviour
-----------------

After setup, the agent is instructed to:

- route raw journal entries or pasted conversations through `_Inbox/` and `_Sessions/`;
- split useful material into atomic topical Markdown files;
- keep the knowledge map, lessons log, and quiz bank current;
- track artifact iterations if the project includes building or shipping something;
- refuse random iteration after failures until a root-cause hypothesis has been logged;
- rebuild the static HTML site after Markdown changes;
- steer the user toward missing prerequisites when needed.

Intended Audience
-----------------

This prompt is for people who want an AI agent to act as a careful teacher, curriculum tracker, Markdown knowledge-base maintainer, and disciplined project-iteration partner.

It is especially suited to projects where the user wants to learn a complex domain from first principles while preserving a durable record of lessons, questions, decisions, failures, and reusable concepts.

It is not intended to be dropped into an existing document archive or software repository.