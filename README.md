# 红包题库 · 社区共建仓库（独乐乐不如众乐乐）

> 这是 HDHive Telegram 红包答题的 **社区共建题库** 模板仓库。
> 把本目录推送到一个新的公开 Git 仓库（GitHub / Gitee 均可），任何人都能通过 Pull Request 贡献题目，管理员合并后，HDHive 后端会按设定的定时器自动拉取并导入题库。

题干固定为 **「独乐乐不如众乐乐」**——好题大家一起出，独享不如共享。

---

## 🧭 工作流

```
贡献者 fork → 编辑 questions/*.json → 提 PR
        │
        ▼
管理员 review → 合并到默认分支
        │
        ▼
HDHive 后端定时拉取归档（.tar.gz）→ 解析 questions/ 下所有 JSON
        │
        ▼
按内容指纹去重 → 新题导入到题干「独乐乐不如众乐乐」
```

- **幂等导入**：每道题按 `题型 + 题干 + 答案 + 选项` 生成指纹去重，重复拉取不会产生重复题目。
- **只增不删**：同步只新增题目，不会删除后端已有题目。下线某题请在后端后台操作。
- **自动建题干**：首次同步时后端会自动创建题干「独乐乐不如众乐乐」，无需手动准备。

---

## 📁 目录结构

```
.
├── README.md                         本说明
├── CONTRIBUTING.md                   贡献指南（提交规范）
├── questions/                        题库目录（后端递归读取此目录下所有 *.json）
│   └── example.json                  示例题库文件
├── schema/
│   └── question-bank.schema.json     JSON Schema，可用于编辑器校验
└── .github/
    └── PULL_REQUEST_TEMPLATE.md      PR 模板
```

> 你可以在 `questions/` 下任意分文件、分子目录组织，例如 `questions/movie/2026.json`、`questions/common.json`，后端会全部读取。

---

## ✍️ 题目格式

每个 JSON 文件可以是一个 **题目数组**，或包含 `questions` 数组的对象：

```json
{
  "questions": [
    {
      "question_text": "下列哪一项是 HDHive 的吉祥物？",
      "question_type": "single_choice",
      "options": ["蜜蜂", "蚂蚁", "蝴蝶", "蜻蜓"],
      "answer": "A",
      "is_active": true
    },
    {
      "question_text": "独乐乐不如众乐乐出自《孟子》。",
      "question_type": "true_false",
      "answer": "对"
    }
  ]
}
```

### 字段说明

| 字段 | 必填 | 说明 |
|---|---|---|
| `question_text` | 是 | 题干文字（也可用 `title`） |
| `question_type` | 否 | `single_choice`（单选）或 `true_false`（判断）。缺省时按选项数量自动推断：4 个选项→单选，2 个选项→判断 |
| `options` | 单选必填 | 单选题必须 **恰好 4 个** 选项，互不相同、非空 |
| `answer` | 是 | 单选可填选项原文或字母 `A/B/C/D`；判断题填 `对` / `错`（也接受 `正确/错误/true/false`） |
| `image_url` | 否 | 题目配图的可公开访问 URL |
| `is_active` | 否 | 是否启用，默认 `true` |

> ⚠️ 校验规则与后端一致：单选题必须 4 个选项且答案匹配其中之一；判断题答案只能是 `对` 或 `错`。不合规的题目会在导入时被跳过并记入失败计数，不影响其他题目。

---

## 🚀 把本模板变成你的社区仓库

1. 新建一个公开仓库，将本目录内容推送上去（默认分支建议 `main`）。
2. 在 HDHive 管理后台 → 红包题库 → **Git 社区同步**：
   - 填写仓库地址（如 `https://github.com/你的组织/red-packet-quiz`）
   - 设置分支（默认 `main`）、子目录（默认 `questions`）
   - 设置定时器 cron（标准 5 段，如 `0 4 * * *` 表示每天 04:00）
   - 打开开关，或点击「立即同步」先试一次
3. 之后社区贡献者提 PR，你合并即可，系统按时自动导入。

---

## 📜 许可

题库内容默认以 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 共享，提交即表示你拥有该内容的权利并同意以此协议分享。可按需替换为你偏好的协议。
