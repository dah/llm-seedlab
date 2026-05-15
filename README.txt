Teaching Knowledge Base Seed Prompt
===================================

This repository contains a seed prompt for creating a personalized teaching knowledge base with an AI agent such as Claude or Cowork.

The prompt is meant to be pasted as the first message in a fresh agent session. The agent then interviews the user about a specific learning domain, proposes a topic structure, and waits for approval before creating anything.

What It Builds
--------------

The generated project is a structured markdown knowledge base with three possible streams:

1. Learning
   A curriculum tracker that records what the user knows, what remains unclear, what has been taught, and every test question asked.

2. Iteration
   An optional artifact-building stream for designs, drafts, experiments, prototypes, releases, or similar work. Failed iterations are not patched randomly; the agent must first record a falsifiable root-cause hypothesis and run a cheap discriminating check.

3. Topical Store
   A durable collection of atomic markdown notes, organized by topic folders and linked back to learning sessions and iteration records.

The project also includes an _Inbox for raw dumps and a _Sessions archive for immutable original session records.

How the Prompt Works
--------------------

The prompt guides the agent through four phases:

Phase 1: Interview
The agent asks about the topic, goal, starting point, bottleneck, definition of success, project slug, file location, and any artifact/iteration workflow. It then proposes topical folders and waits for the user's approval.

Phase 2: Build the Skeleton
After approval, the agent creates the markdown folder structure, including CLAUDE.md, INDEX.md, Meta files, Learning files, optional Iteration files, and topical folder README files.

Phase 3: Wire Up the HTML Site
The agent creates a sibling site folder containing a Python build script named build.py. This script renders the markdown knowledge base into a static HTML site with navigation, breadcrumbs, front matter display, syntax highlighting, MathJax support, and rewritten markdown links.

Phase 4: Kick Off
The agent stores project memory, runs an initial diagnostic quiz, updates the knowledge map, logs the results, and proposes the first real lesson.

Ongoing Behavior
----------------

After setup, the agent is instructed to:

- Route raw journal entries or pasted conversations through _Inbox and _Sessions.
- Split useful material into atomic topical markdown files.
- Keep the Learning knowledge map, lessons log, and quiz bank current.
- Track artifact iterations if the project includes building or shipping something.
- Refuse random iteration after failures until a root-cause hypothesis has been logged.
- Rebuild the static HTML site after markdown changes.
- Proactively steer the user toward missing prerequisites when needed.

Important Note Before Use
-------------------------

This is not just a passive writing prompt. The enclosed prompt instructs the agent to create folders and files, and in Phase 3 it specifically instructs the agent to create a Python program named build.py and run it to generate a static HTML site.

Before using this prompt, make sure you and anyone else affected by the project are comfortable with the agent creating files, writing a Python program, installing or using Python dependencies, and running that program in the chosen workspace. The prompt itself tells the agent not to create anything until the interview is complete and the user has approved the proposed topic spine, but users should still review this behavior before proceeding.

Intended Audience
-----------------

This prompt is useful for people who want an AI agent to act as a careful teacher, curriculum tracker, markdown knowledge-base maintainer, and disciplined project iteration partner.

It is especially suited to projects where the user wants to learn a complex domain from first principles while preserving a durable record of lessons, questions, decisions, failures, and reusable concepts.
