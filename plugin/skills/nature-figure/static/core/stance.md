# Default Stance

## Design Principles

### 1. Clarity Over Beauty

The figure must communicate the conclusion clearly. Aesthetic polish is secondary.

### 2. Hero Panel

Each figure has ONE dominant element that draws the eye. Don't compete for attention.

### 3. Restrained Palette

Use 3-5 colors maximum. Default palette:

```python
COLORS = {
    'primary': '#2563EB',    # Blue - main concepts
    'secondary': '#7C3AED',  # Purple - secondary
    'accent': '#059669',     # Green - supporting
    'warning': '#D97706',    # Orange - emphasis
    'danger': '#DC2626',     # Red - alert
    'text': '#1E293B',       # Dark - text
    'light': '#E2E8F0',     # Light - borders
    'bg': '#F8FAFC',        # Gray - background
}
```

### 4. Typography

- Title: 16pt, bold
- Labels: 10-12pt, normal
- Annotations: 8-9pt, italic
- Minimum print size: 6pt

### 5. Accessibility

- Use colorblind-safe palette (avoid red-green only)
- Add patterns/textures when possible
- Ensure sufficient contrast (4.5:1 minimum)

## Anti-Patterns

- Don't use 3D charts (distorts data)
- Don't use pie charts for >5 categories
- Don't use rainbow colormaps
- Don't add unnecessary gridlines
- Don't use decorative clipart
