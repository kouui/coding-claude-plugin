---
name: report:review
description: review a report for readability by its intended reader and for well-supported claims
argument-hint: <report-file-path>
model: inherit
disable-model-invocation: false
user-invocable: true
allowed-tools:
context:
agent:
hooks:
---

Review a report (experiment result, comparison, investigation) for a human reader who was not part of the work.
The report must make its point quickly, prove each claim with numbers and concrete examples, and contain nothing
the reader cannot understand or check.

## 0. Before reviewing

- Identify the **reader** (customer, manager, new team member) and the **question** the report answers. Every
  check below is judged from that reader's side.
- Locate the raw data behind the report (outputs, logs, records). Numbers are verified against it, not against
  the author's memory.

## 1. Structure: conclusions first, evidence after

Expected order:

1. **Summary:** the main conclusions, 3–5 items, each one sentence plus a pointer to its section. End with the
   author's opinion stated plainly.
2. **One section per conclusion:** the claim, then the numbers that support it, then concrete examples from the
   data that show what the numbers mean.
3. **Overall statistics:** the full tables, after the conclusions, for readers who want the whole picture.
4. **Other findings:** notable cases that are not part of the main conclusions but that the reader should know.
5. **Method / background:** short, written for the reader. It can come before or after the conclusions.

Flag:
- a report organized by how the work was done (by test, script or phase) instead of by conclusion;
- conclusions buried after tables;
- a missing opinion, or an opinion that does not follow from the evidence.

## 2. Summary

- **Every number in the summary is readable without the body.** Either state in the same sentence what it
  measures, or leave it out. A bare figure in parentheses means nothing before the reader has seen the section
  that defines it.
- Each item states the direction and size of the effect, and its limits ("only under condition X").

## 3. Each claim

- **Backed by both numbers and examples.** Numbers alone do not show what the difference looks like in practice.
  Add concrete examples:
  - before vs after, or A vs B, on the same input;
  - with a short explanation of what is good or bad in the example.
- **Precise, not vague.** Replace qualitative words ("small effect", "much better") with direction and size. If
  two effects pull in opposite directions, state both and the net result ("X is N% lower per unit, but usage is
  higher, so the total is M% higher").
- **Scoped correctly:**
  - if an effect appears only under some conditions, say so in the claim;
  - when an aggregated table and a per-condition table seem to disagree, break the numbers down by condition and
    explain before claiming anything.
- **Not stronger than the data:**
  - separate what is proven from what is likely;
  - name the check that would settle the open part;
  - check causal wording ("because X") against the data;
  - check that each metric really measures what the text says. Automatic counters and heuristics can produce
    false positives, so inspect a sample of the counted cases.
- **Only necessary evidence.** Remove data points the argument does not need. Weak or non-comparable baselines
  invite doubt.
- **Not an artifact of the measurement.** If a reported failure comes from how the data was collected (test
  setup, stopping rule, tooling), drop it from the reader-facing version or label it as a limitation of the
  measurement.

## 4. Numbers and tables

- **Every count has a clear total and composition:** "N items in total (a + b × c)", not just "N items". If
  sizes differ between the compared subjects, give each.
- **Every row says what it measures** and, where it is not obvious, why it matters.
- **Rows that sound alike are told apart explicitly**, with what each one includes and excludes.
- **A ratio stated for several subjects is correct for each of them**, not just for one.
- **Percentages and derived values are recomputed** from the raw data.
- **Tables do not contradict each other.** If they seem to, the text explains the difference in scope.

## 5. Reader-facing language

- **No internal identifiers:** script or file names, run labels, version tags, commit hashes, paths, ticket or
  review IDs, internal field names. Describe the content instead ("the scenario where …").
- **No unexplained jargon.** Define a term at first use, or replace it.
- **One term per concept**, and no term reused for two concepts, including section titles that collide with a
  defined term.
- **Out-of-scope content removed.** Alternatives the reader did not ask about, or that were dropped, should not
  appear.
- **Language quality:**
  - no words, characters or grammar from another language mixed in (for Japanese: no Chinese words or
    simplified characters);
  - consistent register and style throughout;
  - no literal translations that read unnaturally;
  - counts and ratios written in the language's natural form.

## 6. Workflow

1. Read the whole report once as the target reader, and note where you got lost or had to guess.
2. Check the structure (section 1) and the summary (section 2).
3. Run two independent reviews in parallel (subagents), because they need different skills:
   - **Language and readability:** sections 2 and 5, plus whether the meaning matches the source if the report
     is a translation.
   - **Values and claims:** sections 3 and 4. Recompute every number from the raw data and check every claim
     against it.
4. Verify the reviewers' findings yourself before applying them. Reviewers can be wrong too, especially when they
   infer facts indirectly instead of checking the primary record.
5. Report the findings grouped by severity:
   - **must fix:** wrong numbers, unsupported claims, contradictions;
   - **should fix:** unclear or misleading wording, missing scope;
   - **optional:** style.

   For each finding give the location, the current text, the problem and a suggested replacement.

## 7. Output

- A short verdict: does the report answer its question for its reader?
- The findings list (section 6, step 5).
- The proposed new outline, if the structure needs to change.

Do not edit the report unless the user asks. If you do, keep the user's own edits to the report.
