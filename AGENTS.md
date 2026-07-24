# AGENTS

本文件描述本仓库内人工协作者与自动化代理协作时应遵循的最小约定。

## 仓库目标

本仓库是一个可同步的 `md-quiz` 仓库，当前采用如下正式结构：

```text
.
├── md-quiz-repo.yaml
├── README.md
├── AGENTS.md
├── quizzes/
│   └── <quiz_id>/
│       ├── quiz.md
│       └── assets/
└── skills/
```

## 何时参考哪个 Skill

- 用户只提“维护问卷”或“维护 md-quiz 仓库”时，优先从 [`skills/md-quiz/SKILL.md`](./skills/md-quiz/SKILL.md) 进入，再分流到下层 skill。
- 编辑或修订 `quizzes/*/quiz.md` 的题目内容、QML 语法、`[rubric]`、`answer_time`、首尾图片时，优先参考 [`skills/qml-authoring/SKILL.md`](./skills/qml-authoring/SKILL.md)。
- 编辑 `md-quiz-repo.yaml`、调整 `quizzes/<quiz_id>/` 目录结构、资源路径或同步约束时，优先参考 [`skills/quiz-repo-spec/SKILL.md`](./skills/quiz-repo-spec/SKILL.md)。

## 编辑规则

- `md-quiz-repo.yaml` 的 `schema_version` 保持为 `2`。
- `md-quiz-repo.yaml` 中的 quiz 路径必须是 `quizzes/<quiz_id>/quiz.md`。
- 新增或删除 `quizzes/<quiz_id>/` 问卷后，必须同步更新 `md-quiz-repo.yaml` 中的 `quizzes` 列表，并更新 `README.md` 中对应的结构示例、问卷列表或相关说明。
- `quizzes/<quiz_id>/quiz.md` 的 Front Matter `id` 必须与目录名 `<quiz_id>` 一致。
- `quizzes/<quiz_id>/quiz.md` 可使用 `tags` 保存 quiz 级标签，推荐写成 YAML 字符串列表，并与问卷主题保持一致。
- QML 文档保持 `format: qml-v2`，并建议同时维护 `schema_version: 2`、`question_count`、`question_counts`、`estimated_duration_minutes`。
- 资源文件只放在当前 quiz 目录下的 `assets/` 中，题面引用统一使用 `./assets/...`。
- `single` 与 `multiple` 题使用 `## Qn [type] (points)`，`short` 题使用 `## Qn [short] {max=points, ...}`。
- `single` 若使用 `{scoring=traits}`，则表示无正确答案的量表题；这类题统一使用 `(0)`，且不得使用 `*`。
- `single` 或 `multiple` 若使用 `{scoring=completion}`，则表示作答计分题；这类题必须使用正分值，不设置正确答案，不使用 `*`，也不得写选项级 `traits`。
- Front Matter 支持 `exam_mode` 字段，控制答题模式：`linear`（逐题，默认）、`full`（全卷通览）。
- `short` 题必须包含 `[rubric]...[/rubric]`。
- `answer_time` 使用 `s`、`m`、`h`，并保持在 parser 允许范围内。
- 首题前和末题后如需展示欢迎图或结束图，只放单独一张 Markdown 图片。

## 修改后的最小检查

- 检查题号是否连续且唯一。
- 检查 `[rubric]` 与 `[/rubric]` 是否成对闭合。
- 检查图片路径是否都指向当前 quiz 的 `./assets/`。
- 检查 `tags` 是否为 YAML 字符串列表，且能准确描述该问卷主题。
- 检查启用 `{scoring=traits}` 的 `single` 题是否没有 `*`，且选项 `traits` 只使用约定的 trait key。
- 检查启用 `{scoring=completion}` 的 `single` / `multiple` 题是否没有 `*`、没有选项级 `traits`，且至少有一个可选项。
- 检查题量统计与预计时长是否和实际题目一致。
- 若新增、删除或重命名问卷，检查 `md-quiz-repo.yaml` 与 `README.md` 是否已同步反映该变更。
- 若改动仓库结构或 manifest，确认 `README.md` 中的说明没有过期。
