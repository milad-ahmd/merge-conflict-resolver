> [!NOTE]
> **This skill lives in the main collection: [milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills/tree/main/skills/merge-conflict-resolver)**. Please ⭐ star it there; that's where updates land first.
> Docs: **https://milad-ahmd.github.io/agent-skills/skills/merge-conflict-resolver/** · Claude Code: `/plugin install all-skills --marketplace milad-ahmd/agent-skills`

<div align="center">

# 🔀 merge-conflict-resolver

**Resolves merge, rebase and cherry-pick conflicts by reading what each side meant, then regenerates lockfiles. An Agent Skill for Claude Code, Cline, Cursor, Codex and other AI coding agents.**

[![License: MIT](https://img.shields.io/github/license/milad-ahmd/merge-conflict-resolver)](LICENSE)
[![Stars](https://img.shields.io/github/stars/milad-ahmd/merge-conflict-resolver?style=social)](https://github.com/milad-ahmd/merge-conflict-resolver)
![Category](https://img.shields.io/badge/category-Git%20&%20Workflow-blue)
![Works with](https://img.shields.io/badge/works%20with-Claude%20Code%20%7C%20Cline%20%7C%20Cursor%20%7C%20Codex-8A2BE2)

[Install](#-install) · [Usage](#-usage) · [How it works](skills/merge-conflict-resolver/SKILL.md) · [All skills](https://github.com/milad-ahmd/agent-skills)

</div>

> Part of **[agent-skills](https://github.com/milad-ahmd/agent-skills)**, a growing collection of practical skills for AI coding agents.

## 📦 Install

**One command (installs the whole collection):**

```bash
curl -fsSL https://raw.githubusercontent.com/milad-ahmd/agent-skills/main/install.sh | bash -s -- merge-conflict-resolver
```

**Manually (Claude Code):**

```bash
git clone https://github.com/milad-ahmd/merge-conflict-resolver /tmp/merge-conflict-resolver
mkdir -p ~/.claude/skills && cp -r /tmp/merge-conflict-resolver/skills/merge-conflict-resolver ~/.claude/skills/
```

**Per project:** copy `skills/merge-conflict-resolver` into `<project>/.claude/skills/`.
**Any other agent:** paste [`SKILL.md`](skills/merge-conflict-resolver/SKILL.md) into your rules or system prompt.

## 💬 Usage

Just ask your agent:

```text
My rebase stopped with CONFLICT in 4 files, help me fix it
package-lock.json is conflicted after merging main, what do I do?
```

The full workflow, rules and output format are in [`SKILL.md`](skills/merge-conflict-resolver/SKILL.md).

## 🔎 Sample output

`conflicts.py` is plain Python 3 with no dependencies and only reads. Real output on a small repo where a rebase stopped: main changed `fetch` to take endpoint paths, the feature branch added retries to it:

```text
$ python3 conflicts.py

Operation: rebasing feature onto main, commit 1/1: 4dc36b4 Retry flaky GETs up to 3 times (#412)
  ours   = HEAD (the branch you rebase onto, main, plus commits already replayed)
  theirs = 4dc36b4 (your commit from feature being replayed)
  continue: git rebase --continue    abort: git rebase --abort
Conflicted files: 1, marker hunks: 1, conflict style: merge

== client.py  [content] both modified
   ours commits:
     950b471 2026-09-18 Take endpoint paths instead of full URLs; lower default timeout
   theirs commits:
     4dc36b4 2026-09-17 Retry flaky GETs up to 3 times (#412)
   hunk 1, lines 6-12
     ours (HEAD):
      def fetch(endpoint, timeout=10):
          resp = http.get(BASE + endpoint, timeout=timeout)
     base, from git merge-file --zdiff3:
      def fetch(url, timeout=30):
          resp = http.get(url, timeout=timeout)
     theirs (4dc36b4 (Retry flaky GETs up to 3 times (#412))):
      def fetch(url, timeout=30, retries=3):
          resp = http.get(url, timeout=timeout, retries=retries)
```

The agent then keeps both intents (`def fetch(endpoint, timeout=10, retries=3)`), and `conflicts.py --check` must exit 0 before `git add`. Exit codes: `0` nothing to resolve, `1` conflicts present, `2` not a git repository.

## 🧩 More skills

See the full collection: **[milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills)**.

## 🤝 Contributing

This repo is a read-only mirror. Please open issues and PRs in **[milad-ahmd/agent-skills](https://github.com/milad-ahmd/agent-skills)**.

## 📄 License

[MIT](LICENSE) © Milad Ahmadi

<div align="center">

**If this skill saved you time, a ⭐ helps others find it.**

</div>
