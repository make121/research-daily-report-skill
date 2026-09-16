# Research Daily Report Guidelines

## 1. What this report is

The report is a compressed reconstruction of the day's research and engineering
reasoning.

It is NOT:

- a Git changelog
- a list of modified files
- a bug-fix report
- a transcript summary
- a list of Codex answers
- a project progress advertisement

The unit of organization is a "problem-solving thread".

---

## 2. Recover hidden reasoning from conversation

User questions often reveal more useful information than code.

Example:

"学生策略和教师表现差不多，是不是说明多技能本身其实能学，只是切换状态
覆盖率不够？"

This contains:

Observation:
Student behavior is qualitatively similar to teacher behavior.

Inference:
The current bottleneck may not be basic multi-skill learnability.

New hypothesis:
Insufficient cross-skill state coverage may be more important.

Report this reasoning while preserving uncertainty.

---

## 3. Track hypothesis evolution

Research often follows:

H1 → experiment → evidence → reject H1 → H2 → experiment → partial support

Preserve this evolution.

Bad:

"排查并解决了 retarget 问题。"

Better:

"最初检查动作是否存在单帧跳变，但回放显示异常旋转是连续发生的，因此
降低了对单帧数据损坏的怀疑。随后将问题定位方向转向关节旋转方向和坐标系
定义，并针对相关旋转处理进行了调整。"

---

## 4. Separate completion and verification

Possible states:

Proposed
Implemented
Executed
Observed
Verified

Do not collapse these states.

Examples:

"修改了奖励函数。"
≠
"新的奖励函数改善了训练效果。"

"重新生成了 retarget 数据。"
≠
"retarget 问题已经解决。"

Only claim improvement/resolution when supported by subsequent evidence.

---

## 5. Preserve useful negative results

Negative results are important when they eliminate possibilities.

Example:

"检查后没有发现姿态的离散跳变，因此问题不像来自单帧异常。"

This is useful progress even though no bug was fixed.

---

## 6. Summarize experiments as causal reasoning

Instead of:

"训练 student policy。"

Prefer:

"为了判断当前问题来自多技能学习能力还是技能切换机制，单独训练 student
policy 进行验证。学生策略表现与教师策略接近，因此当前结果至少表明技能
集合本身具有可学习性，后续排查重点转向切换状态覆盖和恢复机制。"

This captures:

why → experiment → result → interpretation.

---

## 7. Avoid overclaiming

Use calibrated language.

Strong evidence:
"验证表明……"

Moderate evidence:
"结果支持……"

Weak evidence:
"目前更倾向于……"
"初步判断……"

Hypothesis:
"推测……"
"可能与……有关"

Unknown:
"目前尚无法确认……"

---

## 8. Daily conclusion

The conclusion should describe what became clearer today.

Good:

"今天的实验将问题范围从‘多技能是否可学习’进一步缩小到‘切换状态覆盖和
异常状态恢复’。"

Bad:

"今天完成了大量工作并取得良好进展。"

---

## 9. Next steps

Prefer concrete next steps derived from unresolved questions.

Good:

"重新回放修正后的 get-up 数据，检查左腿朝向是否恢复正常，并确认修改
没有影响其他起身序列。"

Bad:

"继续优化模型。"