# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

A marketplace of Claude Code plugins. No build system — entirely Markdown prompts and JSON config.

## Structure

Plugins live under `plugins/<name>/` with a `.claude-plugin/plugin.json` manifest, plus `commands/`, `skills/`, `agents/`, and `hooks/` directories. See `CONTRIBUTING.md` for plugin requirements.

## Evals

Each skill can have `evals/evals.json`. Eval runs produce `*-workspace/iteration-N/` directories with `benchmark.json` comparing with/without skill performance.
