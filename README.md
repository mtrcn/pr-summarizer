# PR Summarizer

An agent skill that explains what a pull request changes, highlights architectural decisions and critical impact, and points reviewers to the code that matters most.

## What you get

- A brief explanation of the problem and resulting behavior
- Major changes described as before → after
- Design, architecture, and UI changes where relevant
- Breaking changes, migration needs, rollout considerations, and review risks
- Links to the files and functions worth inspecting first
- Test evidence and unresolved questions

Output is GitHub-flavored Markdown. When requested, the agent posts it as a general PR comment. It does not approve PRs or change code.

## Install in Codex

Ask Codex:

```text
Use skill-installer to install skills/pr-change-briefing from mtrcn/pr-summarizer.
```

Alternatively, copy `skills/pr-change-briefing` into your personal Codex skills directory.

## Usage

```text
$pr-change-briefing Explain https://github.com/OWNER/REPO/pull/123.
```

```text
$pr-change-briefing Explain PR 123 in OWNER/REPO and post the briefing as a comment.
```

The agent needs read access to the repository and write access to PR comments when posting. It can use a connected GitHub tool or an authenticated GitHub CLI. Local branch diffs can also be summarized without publishing.

## Approach

The skill reads the actual diff and relevant surrounding code, organizes the explanation by behavior and responsibility, and links claims to evidence. It distinguishes observed behavior from inferred intent and reports missing context. A briefing helps focus human review; it does not establish that a change is correct.

## Inspiration

This skill combines the structured change-analysis approach of [summarize-diff-for-agents](https://github.com/vyoungnyc/claude-skills-agents-commands/blob/main/skills/summarize-diff-for-agents/SKILL.md) with the architectural narrative approach of [summarize-pr-architecture](https://github.com/pimlock/eng-skills/blob/main/skills/summarize-pr-architecture/SKILL.md), using a Markdown PR comment instead of an HTML report.
