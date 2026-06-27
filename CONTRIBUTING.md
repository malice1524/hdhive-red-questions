# 贡献指南

感谢参与「独乐乐不如众乐乐」红包题库共建！请按以下规范提交，方便管理员快速 review 合并。

## 提交步骤

1. Fork 本仓库并新建分支，如 `add-movie-questions`。
2. 在 `questions/` 目录下新增或修改 `*.json` 文件。
3. 本地用 `schema/question-bank.schema.json` 校验格式（多数编辑器可自动提示）。
4. 提交 Pull Request，填写 PR 模板。

## 题目质量要求

- **真实、准确**：答案需正确无歧义；有争议或主观题不予合并。
- **健康合规**：禁止政治敏感、色情、暴力、人身攻击、广告引流等内容。
- **去重**：提交前请大致检索，避免与现有题目重复（系统也会按内容指纹自动去重）。
- **单选题恰好 4 个选项**，互不相同；判断题答案只能是 `对` / `错`。
- **配图**（可选）需为可长期公开访问的 URL，建议使用稳定图床。

## 文件组织建议

- 按主题分文件：`questions/common.json`、`questions/movie.json` 等。
- 单个文件不要过大（建议每文件 < 2MB，单题文件总量受后端上限保护）。
- JSON 使用 UTF-8、2 空格缩进。

## 格式速查

```json
{
  "questions": [
    {
      "question_text": "题干……",
      "question_type": "single_choice",
      "options": ["A 选项", "B 选项", "C 选项", "D 选项"],
      "answer": "A",
      "is_active": true
    }
  ]
}
```

字段含义详见仓库根目录 `README.md`。
