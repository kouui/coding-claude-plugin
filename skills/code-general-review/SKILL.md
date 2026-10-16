---
name: code:general-review
description: review code like a human
argument-hint: 
model: inherit
disable-model-invocation: false
user-invocable: true
allowed-tools:
context:
agent:
hooks:
---

# Code review

Goal: make the codebase easier to read, change and reuse a year from now. Not to make this code "safe" against every imaginable input.
Every comment spends the author's maintenance budget. A comment is worth its leverage, not its count; if nothing is worth changing, say so.

## Model first, then comment
Read enough context (callers, callees, related types, neighboring files), then write down in 3 lines:
- What this code is responsible for; whether it is a hub (depended on from many places) or an edge (takes external input / IO / third parties)
- Where data enters, where it is validated, and which invariants hold after that
- The most likely next change in requirements
Base every comment on this model. Context you could not read is an assumption, not a problem.

## Order: existence → placement → shape
Not a checklist; skip any item with nothing to report.
1. Should it exist: dead code, unused parameters / config, abstractions with a single implementation, extension points for imagined needs, stale compatibility layers.
2. One fact, one place: the same rule / constant / format / state written in several places, so every bug fix has to be applied to each copy.
3. Where constraints live: external input is validated once at the boundary and turned into precise types; the interior trusts the invariants. Defensive checks scattered everywhere are a symptom of a missing boundary. Do not push the caller's responsibility down into the callee.
4. Do types express the invariants: bare str / dict / Any, combinations of optional fields, sentinel values and multiple boolean flags let illegal states be represented. Prefer making them impossible to construct over checking them at the point of use.
5. Hub interfaces: narrow, conceptually uniform, semantically stable. A parameter, flag or special case added for one caller moves that caller's complexity into the hub. When two callers disagree, first suspect one of them is wrong.
6. Split along change: what changes together stays together; what changes for different reasons is separated. Over-splitting, and layers that add indirection without hiding any complexity, are as harmful as tangling. Walk through "the next change": how many places must be touched?
7. Failure semantics: which failures should be loud, which are recovered and at which layer; is this consistent with the surrounding code. Swallowed exceptions and every call site wrapping its own try are symptoms.
8. Navigability: can you find the code by name, and guess where the next change of this kind goes; is each concept always called by the same name; does it follow the codebase's existing conventions — a local optimum that breaks convention is usually worse globally.

## Bugs and edge cases
Report real bugs, but give the trigger path: where the input / state comes from, which call chain brings it here, and what the consequence is. Without a path it is not a defect; at most list it as an open question.
"This could be None / empty / out of range" is where an investigation starts, not a comment. Once it is confirmed reachable, first ask at which layer it should be eliminated (boundary, type, caller), and only then consider a check in place.

## Direction of suggestions
Order of preference: leave it > delete or narrow the contract > move the constraint to the boundary or into the type > restructure (move / merge / split / rename) > add code.
When suggesting a new branch, parameter, flag, try/except or retry, explain why every option ranked above it does not work.
Complexity must be proportionate to the problem: if the harm is hypothetical and the cost is certain, leave it.
Give direction, not patches. Review only what this change touches or makes worse; pre-existing debt gets at most one line, marked non-blocking.

## Output
**Model**: the 3 lines above.
**Verdict**: merge / merge after changes / rework, with a one-sentence reason; the single most worthwhile change.
**Findings** (0–5, one per root cause, ordered by impact), each:
- [must | should | optional] location — problem (stated as incorrect behavior with its trigger path, or as "what changing this later will cost")
- Root cause: points at the design (contract / data model / responsibility / dependency), not at this line
- Suggestion: one action; state whether it is a net addition or a net reduction of code
Levels: must = an error with a trigger path, or a structural problem that will keep causing mistakes in later changes; should = leaving it will keep raising maintenance cost; optional = local improvement.
**Open questions** (optional): suspicions without enough evidence, and what information is missing.
**Deliberately not changed** (optional, ≤3, one line each): things you noticed but judged not worth changing, with the reason.
Do not report what a linter / formatter would catch. Do not summarize strengths.
