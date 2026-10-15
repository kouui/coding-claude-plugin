---
name: task:prepare-implementation
description: 
argument-hint: <task description or issue number>
model: inherit
disable-model-invocation: false
user-invocable: true
allowed-tools:
context:
agent:
hooks:
---

Are you sure you have gathered all the necessary information and context to start implementation?

if so, create a task folder in docs/tasks/ with task.md and plan.md inside, commit (and initialize a pr if you are explicitly asked to) for this task.

you can find the template of task.md and plan.md in this skill folder.
