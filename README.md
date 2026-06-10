# Nature Paper Workflow

基于 Claude Code Skills 的学术论文全流程自动化工作流。

一键完成：**文献检索 → 撰写 → 配图 → 引用 → 润色 → 转 Word**

## 功能概览

本项目包含 11 个 Claude Code Skills，覆盖学术论文写作的完整生命周期：

| Skill | 功能 | 说明 |
|-------|------|------|
| **paper-workflow** | 流程编排器 | 串联所有步骤，一键执行全流程 |
| **nature-writing** | 论文撰写 | Nature 风格学术稿件起草，支持 5 种论文类型 |
| **nature-polishing** | 学术润色 | 英文润色、结构调整、LaTeX 排版修复 |
| **nature-citation** | 引用管理 | 自动检索 Crossref/PubMed，GB/T 7714 格式 |
| **nature-figure** | 科学配图 | Python(matplotlib/seaborn) 或 R(ggplot2) 出图 |
| **nature-academic-search** | 文献检索 | 多源并发检索 CrossRef、PubMed、arXiv |
| **nature-reader** | 论文精读 | 中英双语对照阅读，支持 PDF/DOI/arXiv |
| **nature-response** | 审稿回复 | 自动生成逐条回复信 |
| **nature-reviewer** | 模拟审稿 | 模拟 Nature 审稿人评估 |
| **nature-data** | 数据声明 | Data Availability Statement 生成 |
| **nature-paper2ppt** | 论文转 PPT | 论文自动生成中文 PPT |

## 快速开始

### 1. 安装

将 skills 目录复制到 Claude Code 的 skills 目录：

```bash
# 克隆仓库
git clone https://github.com/ksl-182/nature-paper-workflow.git
cd nature-paper-workflow

# 复制 skills 到 Claude Code 目录
cp -r skills/* ~/.claude/skills/

# 复制共享层
mkdir -p ~/.claude/agents/_shared
cp -r shared/* ~/.claude/agents/_shared/
```

### 2. 安装依赖（文献检索功能需要）

```bash
pip install httpx aiohttp fastmcp
```

### 3. 使用

在 Claude Code 中直接说：

```
写一篇关于 大语言模型在嵌入式系统中的应用 的论文
```

或触发关键词：`写论文`、`生成论文`、`论文全流程`、`毕设论文`、`毕业论文`

## 工作流程

```
用户输入主题
    │
    ▼
┌─────────────┐
│  需求确认    │  确认主题、字数、格式
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  文献检索    │  nature-academic-search
│             │  来源: CrossRef, PubMed, arXiv
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  撰写初稿    │  nature-writing
│             │  输出: paper_draft.md
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  科学配图    │  nature-figure
│             │  输出: figures/
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  引用格式化  │  nature-citation
│             │  GB/T 7714 标准
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  学术润色    │  nature-polishing
│             │  输出: paper_final.md
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  转 Word     │  generate_thesis.py
│             │  输出: paper_final.docx
└─────────────┘
```

## 输出文件

```
D:\Claude code OUTPUT\
├── paper_draft.md          ← 初稿
├── paper_final.md          ← 润色后
├── paper_final.docx        ← Word 版本（含格式）
├── references.bib          ← 检索到的文献
└── figures/                ← 科学配图
    ├── fig1_xxx.png
    ├── fig2_xxx.png
    └── ...
```

## 论文类型支持

| 类型 | 说明 |
|------|------|
| research | 原创研究论文 |
| methods | 方法学论文 |
| hypothesis | 假说论文 |
| algorithmic | 算法论文 |
| review | 综述论文 |

## 单独使用各 Skill

每个 Skill 都可以独立使用：

```bash
# 只做文献检索
> 搜索关于 transformer 的最新论文

# 只做润色
> 帮我润色这段学术英文

# 只做配图
> 用 matplotlib 画一张实验结果对比图

# 论文精读
> 帮我精读这篇论文 (提供 PDF 或 DOI)

# 论文转 PPT
> 把这篇论文做成中文 PPT
```

## 架构设计

所有 Skills 遵循统一的 **静态/动态分离** 架构：

```
skill-name/
├── SKILL.md              ← 路由器，检测参数并按需加载
├── manifest.yaml         ← 声明参数轴、值、文件路径
├── static/
│   ├── core/             ← 始终加载的核心内容
│   └── fragments/        ← 按参数加载的片段
├── references/           ← 按需加载的深度参考材料
└── scripts/              ← 可执行的 Python 脚本
```

这种设计确保每次调用只加载当前任务所需的片段，而非全部内容。

## 环境要求

- **Claude Code** (CLI 或 IDE 插件)
- **Python 3.10+** (用于脚本执行)
- **uv** (Python 包管理，推荐)
- 可选: **R** (用于 nature-figure 的 R 后端)

## 依赖

文献检索功能需要以下 Python 包：

- `httpx` - HTTP 客户端
- `aiohttp` - 异步 HTTP
- `fastmcp` - MCP 服务器框架

```bash
pip install httpx aiohttp fastmcp
```

## License

[MIT](LICENSE)
