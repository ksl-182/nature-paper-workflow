---
name: nature-figure
description: "Scientific figure and chart creation with matplotlib. Use when: creating figures, generating charts, data visualization, scientific plots. 中文触发：画图、生成图表、论文配图、数据可视化、科学绘图、制作图表、画柱状图、画折线图、画散点图"
---

# Nature Figure Making

Create scientific figures using matplotlib.

## Workflow

### 1. Analyze Requirements

Read the paper/content and identify:
- Which sections need figures
- What type of figure for each (architecture, timeline, comparison, flow, bar, line)
- The core conclusion each figure must convey

### 2. Load Contract

Read `static/core/contract.md` and complete the checklist for each figure.

### 3. Load Design Guidelines

Read `static/core/stance.md` for color palette, typography, and anti-patterns.

### 4. Generate Code

Read `static/fragments/backend/python.md` for matplotlib templates.

Select the appropriate template:
- Architecture → `figure_architecture()`
- Timeline → `figure_timeline()`
- Comparison → `figure_comparison()`
- Flow Chart → `figure_flow()`
- Bar Chart → `figure_bar()`

Customize the template with actual data/labels from the paper.

### 5. Execute and Save

```bash
python generate_figures.py
```

Output to: `D:/Claude code OUTPUT/figures/`

### 6. Insert into Paper

Add markdown reference in the paper:

```markdown
![图 1 标题](D:/Claude code OUTPUT/figures/fig_name.png)
```

## Quick Example

User: "给论文加几张图"

1. Read the paper to identify figure needs
2. Create `generate_figures.py` with appropriate templates
3. Run the script
4. Report which figures were generated and where
