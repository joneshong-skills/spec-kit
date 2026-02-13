[English](README.md) | [繁體中文](README.zh.md)

# spec-kit

A Claude Code skill that guides Spec-Driven Development (SDD) -- transforming feature descriptions into structured specifications, implementation plans, and executable task lists.

## Description

This skill adapts the [GitHub Spec Kit](https://github.com/github/spec-kit) methodology for use as a Claude Code skill. It provides a complete SDD workflow: writing feature specifications, clarifying ambiguities, generating implementation plans, breaking plans into dependency-ordered tasks, analyzing cross-artifact consistency, and executing implementation phase by phase.

## What It Does

- Transforms natural language feature descriptions into structured specifications
- Guides iterative clarification of ambiguities through targeted questions
- Generates technical implementation plans with research, data models, and API contracts
- Breaks plans into dependency-ordered, parallelizable task lists organized by user story
- Performs non-destructive consistency analysis across spec, plan, and tasks
- Executes implementation following task order with progress tracking
- Creates and manages project constitutions for architectural principles
- Generates requirements quality checklists ("unit tests for English")

## Install

Copy the skill directory into your Claude Code skills folder:

```
cp -r spec-kit ~/.claude/skills/
```

Skills placed in `~/.claude/skills/` are auto-discovered by Claude Code. No additional registration is needed.

## Usage

Invoke the skill by asking Claude Code to work with specifications. Example prompts:

- "Write a spec for a real-time chat system with message history"
- "Create a feature specification for user authentication"
- "Generate an implementation plan for the chat feature using Node.js and WebSocket"
- "Break down the plan into tasks"
- "Analyze the spec, plan, and tasks for consistency"

The skill follows the SDD workflow: Specify, Clarify, Plan, Tasks, Analyze, Implement.
