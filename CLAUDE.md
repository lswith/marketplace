# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A marketplace of Claude Code plugins. No build system — entirely Markdown prompts and JSON config.

## Structure

Plugins live under `plugins/<name>/` with a `.claude-plugin/plugin.json` manifest, plus `commands/`, `skills/`, `agents/`, and `hooks/` directories. See `CONTRIBUTING.md` for plugin requirements.

## Skills vs Commands

Skills must be **tool-agnostic** — they describe workflows, decisions, and interaction patterns without referencing specific tools or services (e.g. don't say "Todoist", "fetch from Todoist", or "set a Todoist deadline"). Only commands should reference MCP tools and service-specific APIs. This keeps skills portable and reusable regardless of the underlying tool.

## Evals

Each skill can have `evals/evals.json`. Eval runs produce `*-workspace/iteration-N/` directories with `benchmark.json` comparing with/without skill performance.
