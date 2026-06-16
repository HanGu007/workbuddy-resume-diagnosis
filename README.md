# Resume Diagnosis Skill — 简历多策略诊断

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-green.svg)](https://github.com/HanGu007/workbuddy-resume-diagnosis/releases)
[![Platform](https://img.shields.io/badge/platform-Any%20AI%20Agent-orange.svg)](#支持的平台)

> **拿到简历后，先别急着改——用这套方法论做一次不留情面的诊断。**

## 这是什么？

一个**平台无关的标准化 AI Agent Skill**。将资深 HR 和职业顾问的简历诊断方法论提炼为 AI 可执行的指令集，让任何 AI 平台都能像专业顾问一样诊断简历。

**与普通提示词的区别**：不是一段"帮我改简历"的 prompt，而是一套包含多策略识别、四维诊断、输出规范、质量铁律的完整诊断体系。

## 功能概览

### 🔍 多策略内容识别

不只看文字——印章、证书、数据图表，一个不漏：

- **策略 1**：模型多模态直读 PDF/Word/图片
- **策略 2**：图片元素专项提取（印章/证书/证件照/数据图表）
- **策略 3**：信息遗漏自检清单 + 主动追问机制

### 🎯 四维度专属诊断

| 维度 | 诊断内容 | 输出 |
|------|---------|------|
| **人物画像** | 行业赛道 × 职能定位 × 岗位路线 | 2-3句精准画像 |
| **经验段位** | 应届→管理层 五级定位 | 段位标签 + 诊断侧重说明 |
| **三大问题** | 原文引用 + HR视角 + 改写方向 | 致命/重要/优化 严重度分级 |
| **被埋没亮点** | 隐藏闪光点挖掘 | "如果改写成XX，HR会看到YY" |

### 📄 HTML 诊断报告

A4 单页 7 模块 HTML 报告：

```
报告头部 → 人物画像 → 四维评分卡片 → 三大问题详解 →
被埋没亮点 → 优化优先级 → 页脚
```

### 🚫 质量铁律

- ❌ 禁止通用废话——必须引用原文片段
- ✅ 每条问题必带改写方向
- ✅ HR视角代入——"看到这句时的心理活动"  
- ✅ 报告即操作手册——拿到就能照着改

## 快速开始

### Open Cloud / Cloud Code

```
创建 Agent → 系统提示词粘贴 SKILL.md 全部内容 → 发送简历
```

### CodeEx

```bash
git clone https://github.com/HanGu007/workbuddy-resume-diagnosis.git
# CodeEx → 导入本地 Skill → 选择 SKILL.md
```

### Cursor / Copilot

```bash
# Cursor
cp SKILL.md .cursor/rules/resume-diagnosis.md

# GitHub Copilot
cp SKILL.md .github/copilot-instructions.md
```

### LangChain / OpenAI SDK

```python
system_prompt = open('SKILL.md', encoding='utf-8').read()
messages = [
    {"role": "system", "content": system_prompt},
    {"role": "user", "content": f"请诊断这份简历：\n{resume_text}"}
]
```

### Dify / Coze

创建知识库 → 上传 SKILL.md → 在 Agent 配置中关联该知识库

## 支持的平台

| 平台 | 加载方式 |
|------|---------|
| Open Cloud | 系统提示词 |
| Cloud Code | 系统提示词 |
| CodeEx | 自定义 Skill 导入 |
| Cursor | `.cursor/rules/` |
| GitHub Copilot | `.github/copilot-instructions.md` |
| LangChain | system message 注入 |
| OpenAI SDK | system message 注入 |
| Dify | 知识库 + 提示词关联 |
| Coze | 知识库 + 提示词关联 |
| 任意 LLM API | 粘贴为 system prompt |

## 推荐工作流

```
  提供简历 + JD
       │
       ▼
  ┌─────────────────┐
  │ resume-diagnosis │ ← 本仓库
  │ 多策略诊断       │
  │ → HTML 诊断报告  │
  └────────┬────────┘
           │
           ▼
  ┌─────────────────┐
  │ resume-rewrite   │
  │ 逐条精准改写     │
  └────────┬────────┘
           │
           ▼
  HTML 生成 → PDF 导出 → 投递
```

搭配 [resume-rewrite](https://github.com/HanGu007/workbuddy-resume-rewrite) 形成诊断→改写的完整链路。

## 目录结构

```
.
├── SKILL.md          # Skill 定义文件（核心）
├── README.md         # 本文件
└── LICENSE           # MIT
```

## 设计哲学

| 原则 | 说明 |
|------|------|
| **平台无关** | 纯文本，不锁任何平台 |
| **自包含** | 零外部依赖，一个文件就是全部 |
| **可审计** | 每个结论追溯到原文 + HR视角解读 |
| **可组合** | 与 resume-rewrite 等串联使用 |
| **人类可读** | HR 顾问也能照着这份文档做诊断 |

## 常见问题

**Q: 不连外部 API 怎么识别图片中的印章？**
A: 依赖 AI 模型自身的多模态能力。如果平台不支持多模态，诊断流程会引导用户手动描述图片内容——这是设计上的降级策略。

**Q: 报告必须用 HTML 吗？**
A: SKILL.md 推荐 HTML 以获得专业排版，但 Agent 也可输出 Markdown 或纯文本——诊断逻辑不变。

**Q: 和 resume-rewrite 必须一起用吗？**
A: 不必须，但推荐。诊断告诉你"哪里有问题"，改写帮你"具体怎么改"。各自可独立使用。

**Q: 如何自定义诊断标准？**
A: 直接修改 SKILL.md。纯 Markdown，任何编辑器都能改。

## 贡献

欢迎提 Issue 和 PR。特别欢迎：
- 新增"HR视角解读"案例
- 不同行业的诊断维度补充
- 报告 HTML 模板优化
- 多语言版本

## 许可证

MIT License © 2026 [HanGu007](https://github.com/HanGu007)

---

<p align="center">
  <sub>标准化 AI Agent Skill · 一次编写 · 多平台部署 · 永久开源</sub>
</p>
