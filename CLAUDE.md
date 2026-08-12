# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository purpose

This is a personal practice repository for learning Git/GitHub operations (`githubprac` — see README.md). It is not an application: there is no build, lint, or test tooling, and no source code to compile. Changes here are typically documentation edits, small file additions, and exercises in branching/PR/review workflows.

## Structure

- `README.md` — learning log; tracks which phase of the exercise (branching, PRs, .gitignore, issues, protections, etc.) has been completed.
- `profile.md` — learner's profile notes.
- `config/secret.env` — intentionally gitignored (`config/secret*` in `.gitignore`); used to practice keeping secrets out of version control. Never remove this from `.gitignore` or commit files matching `config/secret*` or `*.env`.
- `pull.txt`, `pull2.txt`, `pull3.txt`, `raiting.txt` — empty placeholder files created during PR/pull exercises; not meant to hold real content.
- `.github/pull_request_template.md` — PR description template (概要/変更内容/確認方法/関連Issue/チェックリスト). Follow its sections when drafting PR bodies for this repo.
- `.github/workflows/check.yml` — "Basic Checks" CI workflow that runs on PRs into `main`:
  - Greps `.md`/`.txt`/`.env` files for secret-like patterns (AWS access keys and common secret-variable assignments — see `check.yml` for the exact regex) and fails the build if found.
  - Greps `.md` files for unresolved conflict markers (`<<<<<<<` / `>>>>>>>`) and fails the build if found.
  - Keep any new Markdown/text content free of these patterns so CI stays green.

## Working conventions

- `main` is protected and requires PR review before merging (per README's learning log: "承認必須ルールの検証" / approval-required rule).
- Commit messages and PR content in this repo are written in Japanese, matching existing history — follow that convention unless told otherwise.
- Since this repo has no code to test, "verification" for a change means: confirm no secret-like strings or leftover conflict markers were introduced (matching what `check.yml` enforces), and that `config/secret.env` remains untracked.

## Rules for Claude Code

1. Never commit or push directly to the `main` branch. Always create a feature branch and merge via a PR.
2. Branch names must follow the format `feature/<description>` or `fix/<description>`.
3. If a push is rejected by a Ruleset, do not bypass it with `--force` or `--admin`. Report the failure and wait for instructions.
4. Do not read `config/secret.env`. Never output its contents to the screen, a PR, or an Issue.
5. Do not include absolute paths (e.g. `/Users/...`) in output. Use paths relative to the repository root.
6. README's learning log is a historical record and may not match the current Ruleset configuration. Treat GitHub's actual settings as the source of truth for governance.
