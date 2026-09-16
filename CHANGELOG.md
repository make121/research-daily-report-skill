# Changelog

本文件记录 `research-daily-report` 技能包的变更历史。

格式参考 [Keep a Changelog](https://keepachangelog.com/zh-CN/1.1.0/)，
版本号遵循 [语义化版本](https://semver.org/lang/zh-CN/)。

## [Unreleased]

暂无。

## [0.1.0] - 2026-09-16

技能包初始版本。

### 新增

- `SKILL.md`：技能定义与完整写作规范，包含
  - 核心原则：以「问题求解过程」而非 Git changelog 作为报告主线
  - 证据来源优先级：对话 → 实验结果 → 终端日志 → 代码改动 → Git 状态
  - 证据分类：`OBSERVED` / `USER_HYPOTHESIS` / `ASSISTANT_SUGGESTION` /
    `ATTEMPTED` / `RESULT` / `SUPPORTED` / `REJECTED` / `SOLVED` /
    `UNRESOLVED` / `NEXT_STEP`
  - 真实性规则：禁止「建议→已执行」「假设→已确认原因」「已尝试→已解决」
    「代码已改→已验证」「计划做→已完成」五类等价替换
  - 任务归并规则：按问题求解线程合并相关事件，不按对话或文件顺序罗列
  - 负结果保留规则：失败的尝试若排除掉某些可能性，必须保留
  - 报告结构与写作风格：默认中文，措辞随证据强度分级
  - 最终一致性自检清单（10 项）
- `references/report-guidelines.md`：补充写作指南，涵盖假设演化、
  证据分级与措辞校准。
- `references/example-report.md`：示例日报，展示期望的推理还原程度。
- `README.md`：项目说明、核心原则、关键约束、目录结构与使用方式。
- `.gitignore`、`.gitattributes`：仓库基础配置。

### 说明

- 面向机器人、强化学习、仿真、算法开发、实验调试与论文复现场景。
- 当前版本尚未指定开源许可证。

[Unreleased]: https://github.com/make121/research-daily-report-skill/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/make121/research-daily-report-skill/releases/tag/v0.1.0
