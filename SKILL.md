---
name: research-daily-report
description: >
  Generate a research/engineering daily report from today's Codex conversations,
  experiments, commands, logs, code changes, and debugging process. Use when the
  user asks to summarize today's work, write a daily report, research log,
  experiment log, debugging summary, or 日报. Reconstruct the reasoning and
  problem-solving process rather than producing a Git changelog or repair report.
---

# Research Daily Report

Generate a daily research/engineering report by reconstructing what the user
actually investigated, tried, observed, inferred, solved, and left unresolved.

The report is intended for robotics, reinforcement learning, simulation,
algorithm development, experiments, debugging, and research reproduction work.

## Core Principle

Do NOT summarize the day as a code-change log.

The primary goal is to reconstruct the user's problem-solving process:

Goal
→ Observation
→ Hypothesis / inference
→ Attempt
→ Result
→ Interpretation
→ Solution
→ Remaining issue
→ Next step

Not every task needs every stage.

Do not mechanically output these labels. Prefer a coherent technical narrative.

A good report should allow the user to understand several weeks later:

1. What was being investigated?
2. Why was it investigated?
3. What phenomenon or problem was observed?
4. What did the user think might be causing it?
5. What approaches were actually attempted?
6. What happened after each attempt?
7. Which hypotheses were supported or rejected?
8. What was actually solved?
9. How was it solved?
10. What remains unresolved?
11. What should be investigated next?

## Evidence Sources

Use all information available in the current Codex environment.

Prefer evidence in roughly this order:

1. User-Codex conversation and user questions
2. Experiment/run/evaluation results
3. Terminal commands and logs
4. Code edits and diffs
5. Git status/diff/commit history
6. Current repository state

Do not rely only on Git changes.

The conversation is particularly important because it often contains:

- experiment motivation
- observations
- hypotheses
- rejected explanations
- reasoning behind an implementation
- interpretation of experimental results
- decisions about what to try next

These may never appear in the source code.

## Reconstruct User Reasoning

Pay special attention to the user's questions.

A question often implicitly contains an observation or hypothesis.

Example:

User:
"The retargeted get-up motion does not jump, but the left hip keeps rotating
until the leg is almost 180 degrees reversed. Could the joint axis be wrong?"

Extract:

Observation:
The abnormal rotation is continuous rather than a single-frame discontinuity.

User hypothesis:
The problem may originate from joint-axis / rotation-direction conventions
rather than an isolated corrupted frame.

Do NOT write:

"The joint axis was wrong."

unless subsequent evidence actually confirms it.

Preserve the distinction between observation, hypothesis, test, and conclusion.

## Evidence Classification

Internally classify important information as:

OBSERVED
Directly observed from experiments, logs, visualization, or user description.

USER_HYPOTHESIS
An explanation proposed or suspected by the user.

ASSISTANT_SUGGESTION
An approach suggested by Codex but not necessarily executed.

ATTEMPTED
Something the user or Codex actually implemented, changed, executed, or tested.

RESULT
The observed outcome of an attempted experiment/change.

SUPPORTED
Evidence increased confidence in a hypothesis.

REJECTED
Evidence contradicted or substantially weakened a hypothesis.

SOLVED
A problem was actually resolved and the result was verified.

UNRESOLVED
A problem remains open or the evidence is insufficient.

NEXT_STEP
A planned or logically motivated follow-up.

These labels are primarily for reasoning. Do not necessarily expose them
literally in the final report.

## Critical Truthfulness Rules

Never convert:

ASSISTANT_SUGGESTION → ATTEMPTED

USER_HYPOTHESIS → CONFIRMED_CAUSE

ATTEMPTED → SOLVED

CODE_CHANGED → VERIFIED

PLANNED → COMPLETED

If Codex suggested three solutions and the user only tested one, report only
that one as attempted.

The other approaches may be mentioned only when useful and clearly described
as alternatives that were considered but not verified.

If a change was implemented but its result was not tested, say:

"已完成修改，效果尚待验证"

rather than:

"问题已解决"

If evidence is insufficient, preserve the uncertainty.

## Task Reconstruction

Group related interactions into meaningful research/engineering tasks.

Do NOT organize the report by conversation order such as:

- Asked question A
- Changed file A
- Asked question B
- Changed file B

Instead merge related events into a problem-solving thread.

For example:

Retargeting problem
  ├─ abnormal left-leg rotation observed
  ├─ inspected motion
  ├─ ruled out frame discontinuity
  ├─ suspected coordinate/joint-axis issue
  ├─ modified rotation handling
  └─ regenerated motion for validation

This should normally become one report section.

## Attempts and Negative Results

Preserve failed experiments and unsuccessful approaches when they contributed
to understanding the problem.

Do not remove them merely because they failed.

A useful failed attempt should explain:

- what was tried
- why it was tried
- what happened
- what was learned

For example:

"最初检查是否存在单帧姿态跳变，但回放发现左腿旋转是连续累积的，因此
暂时排除了单帧异常这一方向，并将排查重点转向关节旋转定义和坐标系转换。"

This is more useful than:

"检查了动作数据。"

## Experiments

For experiments, recover when available:

- experiment objective
- configuration or changed variable
- comparison/baseline
- observed behavior
- quantitative result
- qualitative result
- interpretation
- limitations

Do not invent missing metrics.

If the user gives qualitative observations such as:

"和教师表现类似"

preserve them as qualitative observations unless quantitative evaluation exists.

## Problem Resolution

When a problem was solved, explain both:

### Problem

What failed and how it manifested.

### Diagnosis

How the cause was narrowed down.

### Solution

What was actually changed.

### Verification

What evidence showed that the solution worked.

A code modification alone is not verification.

## Code Changes

Include implementation details only when they help explain:

- an experiment
- a hypothesis test
- a bug fix
- a research decision
- a meaningful capability added

Avoid low-value details such as:

"Modified xxx.py"
"Changed function foo()"
"Updated configuration"

unless those details are technically important.

Prefer:

"为验证关节旋转方向是否导致 retarget 后左腿持续内旋，对对应关节的
旋转方向处理进行了调整，并重新生成动作数据进行回放检查。"

## Report Structure

Do NOT force a rigid template.

Choose sections based on the day's actual work.

Recommended structure:

# YYYY-MM-DD 日报

## 1. [Major task / experiment / problem]

Explain:
- objective/context
- observations
- reasoning
- attempts
- results
- conclusions

## 2. [Another meaningful task]

...

## 今日结论

Summarize only conclusions actually supported by today's work.

## 未解决问题与下一步

Include unresolved issues and concrete follow-up work.

If the day contains only one major problem, one detailed section is better
than artificially creating multiple sections.

## Writing Style

Default language: Chinese, unless the user requests another language.

Use concise professional engineering/research language.

Prefer:

"测试发现……"
"回放中观察到……"
"据此推测……"
"为验证这一判断……"
"进一步测试表明……"
"该结果说明……"
"目前尚不能确认……"
"因此将排查重点转向……"

Avoid excessive phrases like:

"成功完成"
"完美解决"
"显著提升"

unless supported by evidence.

Avoid turning the report into a list of tiny bullet points.

Prefer coherent paragraphs, supplemented by bullets when they improve clarity.

## Detail Selection

High priority:
- important observations
- user reasoning
- hypotheses
- experiment design
- attempted fixes
- failed approaches
- comparison results
- verified solutions
- unresolved technical questions
- next-step decisions

Medium priority:
- meaningful code implementation
- parameter/configuration changes
- dataset changes
- environment changes

Low priority:
- formatting
- trivial refactoring
- repeated commands
- dependency installation
- temporary debugging output

Include low-priority items only when they materially affected the work.

## Final Consistency Check

Before returning the report, verify:

1. Did I reconstruct the reasoning rather than merely list code changes?
2. Did I include important user observations from questions/conversation?
3. Did I distinguish hypotheses from confirmed causes?
4. Did I distinguish suggestions from actions actually performed?
5. Did I preserve meaningful failed attempts?
6. Did I describe the results of experiments where available?
7. Did I avoid claiming an unverified fix as solved?
8. Did I identify unresolved issues?
9. Did I capture the next logical or explicitly stated steps?
10. Would this report help reconstruct today's research process weeks later?

If not, revise before returning.

For additional report-writing guidance, read:
references/report-guidelines.md

When examples are useful, read:
references/example-report.md