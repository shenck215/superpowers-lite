# Routing Guide

Use this file when the task sits between two modes and the routing decision is not obvious.

## Fast Scoring

Score the task before choosing a mode.

- Scope
  - `0`: one local edit or one direct answer
  - `1`: multiple related edits in the same area
  - `2`: cross-module or cross-layer work
- Ambiguity
  - `0`: requirement is explicit
  - `1`: one or two assumptions are needed
  - `2`: problem framing or success criteria are unclear
- Risk
  - `0`: low blast radius
  - `1`: moderate behavior risk
  - `2`: architecture, reliability, security, migration, or performance risk
- Diagnosis
  - `0`: no investigation needed
  - `1`: limited inspection needed
  - `2`: root cause is uncertain or competing explanations exist

## Mode Selection

- Total `0-2`: `Quick`
- Total `3-5`: `Standard`
- Total `6-8`: `Deep`

Apply escalation rules before de-escalation rules. If both match, keep the higher-rigor mode.

Escalate one level when any of these are true even if the numeric score is lower:

- The user explicitly asks for a structured review.
- The change touches authentication, authorization, payments, data deletion, migrations, or concurrency.
- The task can break external contracts or backward compatibility.

De-escalate one level when all of these are true:

- The user wants a minimal fix only.
- The affected area is already isolated.
- The implementation path is obvious.

Never de-escalate below `Quick`.

## Canonical Examples

### Quick

- `$superpowers-lite 重构这个小函数，减少重复判断`
- `$superpowers-lite 修复这个接口里空值判断的 bug`
- `$superpowers-lite 帮我给这个 SQL 补一个分页参数`

### Standard

- `$superpowers-lite 帮我实现一个 Node.js 接口，要求支持分页和权限校验`
- `$superpowers-lite 给这个上传接口加文件类型校验和错误码设计`
- `$superpowers-lite 重构这段服务层代码，让职责更清晰`

### Deep

- `$superpowers-lite 设计一个文件上传服务，支持断点续传`
- `$superpowers-lite 帮我分析这个线上报错并给出最小修改方案`
- `$superpowers-lite 重构这个模块，拆掉历史耦合但保持兼容`

## Response Calibration

Choose the lighter mode when both approaches are safe and the user values speed.

Choose the heavier mode when:

- failure cost is high
- rollback is hard
- investigation is the main work
- the user is asking for design quality rather than a narrow patch
