---
name: paper-workflow
description: "论文写作全流程自动化。触发：写论文、生成论文、论文全流程、毕设论文、毕业论文。自动串联 academic-search → writing → figure → citation → polishing → thesis-generator"
---

# 论文写作工作流

一键完成：文献检索 → 撰写 → 配图 → 引用 → 润色 → 转 Word

## 触发条件

用户说以下关键词时自动触发：
- 写论文、生成论文、论文全流程
- 毕设论文、毕业论文
- 帮我写一篇关于 XXX 的论文

## 工作流程

### 步骤 1：需求确认

向用户确认：
- 论文主题
- 字数要求
- 格式要求（默认湖北工程学院格式）
- 是否有实验数据/参考文献

### 步骤 2：文献检索（nature-academic-search）

```
Skill: nature-academic-search
输入：用户提供的主题
输出：相关文献列表（含引用格式）
工作流：multi-source-search
来源：arXiv、PubMed、Google Scholar
```

### 步骤 3：撰写（nature-writing）

```
Skill: nature-writing
输入：用户提供的主题、要求、数据 + 步骤 2 的文献
输出：Markdown 格式论文初稿
位置：D:/Claude code OUTPUT/paper_draft.md
```

### 步骤 4：配图（nature-figure）

```
Skill: nature-figure
输入：步骤 3 的论文内容
输出：科学配图（matplotlib 生成）
位置：D:/Claude code OUTPUT/figures/
```

### 步骤 5：引用格式化（nature-citation）

```
Skill: nature-citation
输入：步骤 3 的论文内容
输出：格式化的参考文献（GB/T 7714）
```

### 步骤 6：润色（nature-polishing）

```
Skill: nature-polishing
输入：步骤 3 + 4 + 5 的内容
输出：润色后的论文
位置：D:/Claude code OUTPUT/paper_final.md
```

### 步骤 7：转 Word（thesis-generator）

```bash
python ~/.claude/skills/HBGC-LW/generate_thesis.py "D:/Claude code OUTPUT/paper_final.md" "D:/Claude code OUTPUT/paper_final.docx"
```

## 输出文件

所有文件输出到 `D:\Claude code OUTPUT\`：

```
D:\Claude code OUTPUT\
├── paper_draft.md          ← 初稿
├── paper_final.md          ← 润色后
├── paper_final.docx        ← Word 版本
├── references.bib          ← 检索到的文献
└── figures/                ← 配图
    ├── fig1_xxx.png
    ├── fig2_xxx.png
    └── ...
```

## 注意事项

- 每个步骤完成后告知用户进度
- 如果用户只需要部分步骤，可以单独执行
- 图片统一输出到 figures/ 子目录
- 最终 Word 文件包含所有图片和格式
- 文献检索是第一步，为后续写作提供支撑
