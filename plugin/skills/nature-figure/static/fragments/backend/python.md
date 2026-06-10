# Python Backend (matplotlib)

## Execution Rule

All figures MUST be generated with matplotlib. No exceptions.

## Quick Start

```python
import matplotlib
matplotlib.use('Agg')  # Non-interactive backend
import matplotlib.pyplot as plt
from matplotlib.patches import FancyBboxPatch
import os

# Global settings
plt.rcParams['font.sans-serif'] = ['SimHei', 'Microsoft YaHei', 'DejaVu Sans']
plt.rcParams['axes.unicode_minus'] = False
plt.rcParams['figure.dpi'] = 200

# Output directory
OUTPUT_DIR = "D:/Claude code OUTPUT/figures"
os.makedirs(OUTPUT_DIR, exist_ok=True)
```

## Common Building Blocks

### Rounded Box

```python
def draw_rounded_box(ax, x, y, w, h, text, color, text_color='white', fontsize=10, bold=False):
    box = FancyBboxPatch((x, y), w, h, boxstyle="round,pad=0.1",
                         facecolor=color, edgecolor='none', alpha=0.95)
    ax.add_patch(box)
    weight = 'bold' if bold else 'normal'
    ax.text(x + w/2, y + h/2, text, ha='center', va='center',
            fontsize=fontsize, color=text_color, weight=weight)
```

### Arrow

```python
def draw_arrow(ax, x1, y1, x2, y2, color='#94A3B8'):
    ax.annotate('', xy=(x2, y2), xytext=(x1, y1),
                arrowprops=dict(arrowstyle='->', color=color, lw=1.5))
```

## Chart Templates

### 1. Architecture Diagram (架构图)

```python
def figure_architecture():
    fig, ax = plt.subplots(figsize=(10, 7))
    ax.set_xlim(0, 10)
    ax.set_ylim(0, 7)
    ax.axis('off')
    ax.set_facecolor('#F8FAFC')
    fig.patch.set_facecolor('#F8FAFC')

    ax.text(5, 6.6, 'Title', ha='center', va='center',
            fontsize=16, fontweight='bold', color='#1E293B')

    # Top layer
    draw_rounded_box(ax, 1.5, 5.2, 7, 1, 'Layer 1\nDescription', '#2563EB')

    # Arrow
    draw_arrow(ax, 5, 5.2, 5, 4.8)

    # Middle layer
    draw_rounded_box(ax, 1.5, 3.6, 7, 1, 'Layer 2\nDescription', '#7C3AED')

    # Arrow
    draw_arrow(ax, 5, 3.6, 5, 3.2)

    # Bottom layer
    draw_rounded_box(ax, 1.5, 2, 7, 1, 'Layer 3\nDescription', '#059669')

    plt.tight_layout()
    plt.savefig(f'{OUTPUT_DIR}/fig_architecture.png', bbox_inches='tight', dpi=200)
    plt.close()
```

### 2. Timeline (时间轴)

```python
def figure_timeline():
    fig, ax = plt.subplots(figsize=(12, 5))
    ax.set_xlim(0, 12)
    ax.set_ylim(0, 5)
    ax.axis('off')

    # Timeline line
    ax.plot([1, 11], [2.8, 2.8], color='#E2E8F0', lw=3, zorder=1)

    phases = [
        (1.5, 3.5, 2.5, 0.8, 'Phase 1\n2018-2020', 'Description', '#2563EB'),
        (4.5, 3.5, 2.5, 0.8, 'Phase 2\n2020-2023', 'Description', '#7C3AED'),
        (7.5, 3.5, 2.5, 0.8, 'Phase 3\n2023-Now', 'Description', '#059669'),
    ]

    for x, y, w, h, title, desc, color in phases:
        draw_rounded_box(ax, x, y, w, h, f'{title}\n{desc}', color, fontsize=9)
        ax.plot(x + w/2, 2.8, 'o', color=color, markersize=10, zorder=2)

    plt.tight_layout()
    plt.savefig(f'{OUTPUT_DIR}/fig_timeline.png', bbox_inches='tight', dpi=200)
    plt.close()
```

### 3. Comparison Table (对比表)

```python
def figure_comparison():
    fig, ax = plt.subplots(figsize=(11, 7))
    ax.set_xlim(0, 11)
    ax.set_ylim(0, 7)
    ax.axis('off')

    headers = ['Col1', 'Col2', 'Col3', 'Col4']
    col_x = [0.3, 2.3, 4.5, 8.5]
    col_w = [1.8, 2.0, 3.8, 2.2]

    # Header row
    for i, (x, w) in enumerate(zip(col_x, col_w)):
        draw_rounded_box(ax, x, 6, w, 0.5, '', '#1E293B')
        ax.text(x + w/2, 6.25, headers[i], ha='center', va='center',
                fontsize=10, color='white', fontweight='bold')

    # Data rows
    data = [
        ['Row1', 'Data1', 'Data2', 'Data3'],
        ['Row2', 'Data4', 'Data5', 'Data6'],
    ]

    for j, row in enumerate(data):
        y = 5.2 - j * 0.7
        bg = '#EFF6FF' if j % 2 == 0 else '#F8FAFC'
        for i, (x, w) in enumerate(zip(col_x, col_w)):
            ax.add_patch(FancyBboxPatch((x, y), w, 0.55, boxstyle="round,pad=0.05",
                                        facecolor=bg, edgecolor='#E2E8F0'))
            ax.text(x + w/2, y + 0.275, row[i], ha='center', va='center', fontsize=9)

    plt.tight_layout()
    plt.savefig(f'{OUTPUT_DIR}/fig_comparison.png', bbox_inches='tight', dpi=200)
    plt.close()
```

### 4. Flow Chart (流程图)

```python
def figure_flow():
    fig, ax = plt.subplots(figsize=(12, 5))
    ax.set_xlim(0, 12)
    ax.set_ylim(0, 5)
    ax.axis('off')

    steps = [
        (0.5, 2.2, 'Step 1', '#2563EB'),
        (3, 2.2, 'Step 2', '#7C3AED'),
        (5.5, 2.2, 'Step 3', '#059669'),
        (8, 2.2, 'Step 4', '#D97706'),
        (10.5, 2.2, 'Step 5', '#DC2626'),
    ]

    for x, y, text, color in steps:
        draw_rounded_box(ax, x, y, 1.8, 1, text, color, fontsize=10, bold=True)

    for i in range(len(steps) - 1):
        draw_arrow(ax, steps[i][0] + 1.8, 2.7, steps[i+1][0], 2.7)

    plt.tight_layout()
    plt.savefig(f'{OUTPUT_DIR}/fig_flow.png', bbox_inches='tight', dpi=200)
    plt.close()
```

### 5. Bar Chart (柱状图)

```python
def figure_bar():
    fig, ax = plt.subplots(figsize=(10, 6))

    categories = ['A', 'B', 'C', 'D', 'E']
    values = [23, 45, 56, 78, 32]
    colors = ['#2563EB', '#7C3AED', '#059669', '#D97706', '#DC2626']

    bars = ax.bar(categories, values, color=colors, width=0.6, edgecolor='none')

    # Add value labels
    for bar, val in zip(bars, values):
        ax.text(bar.get_x() + bar.get_width()/2, bar.get_height() + 1,
                str(val), ha='center', va='bottom', fontsize=10, fontweight='bold')

    ax.set_ylabel('Value', fontsize=12)
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)
    ax.set_facecolor('#F8FAFC')

    plt.tight_layout()
    plt.savefig(f'{OUTPUT_DIR}/fig_bar.png', bbox_inches='tight', dpi=200)
    plt.close()
```

## Export Helper

```python
def save_figure(fig, name, output_dir=OUTPUT_DIR):
    """Save figure with standard settings"""
    path = f'{output_dir}/{name}.png'
    fig.savefig(path, bbox_inches='tight', dpi=200, facecolor=fig.get_facecolor())
    plt.close(fig)
    print(f"Saved: {path}")
    return path
```
