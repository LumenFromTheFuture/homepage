# De Principiis Style Guide

This document describes the design system for De Principiis interactive demos.

## Design Philosophy

- **Accessible**: Light mode by default, with dark mode option
- **Educational**: Clean typography that doesn't distract from content
- **Consistent**: Same patterns across all demos
- **Self-contained**: Each HTML file includes all styles (no external CSS files)

## Theme System

All colors are defined as CSS custom properties, making theming trivial:

```css
:root {
    /* Light theme (default) */
    --bg-primary: #fafafa;
    --bg-secondary: #ffffff;
    --bg-tertiary: #f0f0f0;
    --text-primary: #2a2a2a;
    --text-secondary: #555555;
    --text-muted: #888888;
    --accent: #4a7ab0;
    --accent-hover: #3d6a9c;
    --border: #e0e0e0;
    --shadow: rgba(0, 0, 0, 0.08);
    --canvas-bg: #ffffff;
}

[data-theme="dark"] {
    --bg-primary: #1a1a2e;
    --bg-secondary: #16213e;
    --bg-tertiary: #1c2a4a;
    --text-primary: #e0e0e0;
    --text-secondary: #bbbbbb;
    --text-muted: #888888;
    --accent: #7faadb;
    --accent-hover: #9bc0eb;
    --border: #2a3a5e;
    --shadow: rgba(0, 0, 0, 0.3);
    --canvas-bg: #16213e;
}
```

### Theme Toggle

Include a fixed toggle button and these JavaScript functions:

```javascript
function initTheme() {
    const saved = localStorage.getItem('deprincipiis-theme');
    if (saved === 'dark') {
        document.documentElement.setAttribute('data-theme', 'dark');
        updateThemeUI('dark');
    }
}

function toggleTheme() {
    const current = document.documentElement.getAttribute('data-theme');
    const next = current === 'dark' ? 'light' : 'dark';
    
    if (next === 'dark') {
        document.documentElement.setAttribute('data-theme', 'dark');
    } else {
        document.documentElement.removeAttribute('data-theme');
    }
    
    localStorage.setItem('deprincipiis-theme', next);
    updateThemeUI(next);
}

function updateThemeUI(theme) {
    document.getElementById('theme-icon').textContent = theme === 'dark' ? '🌙' : '☀️';
    document.getElementById('theme-label').textContent = theme === 'dark' ? 'Dark' : 'Light';
}

initTheme();
```

Theme preference persists across all demos via `localStorage`.

## Typography

- **Font family**: `Georgia, 'Times New Roman', serif`
- **Headings**: Normal weight, accent color
- **Body text**: 1.6 line height
- **h1**: 2rem
- **Subtitle**: Italic, muted color

## Layout

### Page Structure

```html
<body>
    <button class="theme-toggle">...</button>
    
    <div class="container">
        <header>
            <div class="breadcrumb">
                <a href="index.html">De Principiis</a> → Principle Name
            </div>
            <h1>Principle Name</h1>
            <p class="subtitle">Short tagline</p>
        </header>

        <main class="main-content">
            <p class="description">...</p>
            
            <div class="simulation-container">
                <!-- Canvas or interactive element -->
            </div>

            <div class="controls">
                <!-- Control panel -->
            </div>
        </main>

        <footer>
            <a href="index.html">← Back to De Principiis</a>
        </footer>
    </div>
</body>
```

### Container

- Max width: 1000px (or 800px for text-heavy pages)
- Horizontal padding: 20px
- Vertical padding: 40px

### Cards/Panels

```css
.panel {
    background: var(--bg-secondary);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 4px 12px var(--shadow);
}
```

## Controls

### Buttons

```css
.btn {
    padding: 10px 20px;
    border: none;
    border-radius: 6px;
    font-family: inherit;
    font-size: 0.9rem;
    cursor: pointer;
    transition: all 0.2s;
}

.btn-primary {
    background: var(--accent);
    color: white;
}

.btn-secondary {
    background: var(--bg-tertiary);
    color: var(--text-primary);
    border: 1px solid var(--border);
}
```

### Sliders

```css
input[type="range"] {
    width: 100%;
    height: 6px;
    border-radius: 3px;
    background: var(--bg-tertiary);
    appearance: none;
}

input[type="range"]::-webkit-slider-thumb {
    appearance: none;
    width: 16px;
    height: 16px;
    border-radius: 50%;
    background: var(--accent);
}
```

### Control Groups

```css
.control-group {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.control-group label {
    font-size: 0.9rem;
    color: var(--text-secondary);
}
```

### Controls Header

```css
.controls-header {
    font-size: 0.85rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    color: var(--accent);
    margin-bottom: 15px;
    padding-bottom: 10px;
    border-bottom: 1px solid var(--border);
}
```

## Canvas/Simulation Colors

For simulations that need their own color scheme (physics simulations, charts), use colors that work in both themes:

- **Positive/growth**: `#4CAF50` or `#70e070`
- **Neutral**: `#4a7ab0` or `#7faadb`
- **Negative/warning**: `#e07070`
- **Objects**: Use gradients for depth

For canvas backgrounds, use `var(--canvas-bg)`.

## Responsive Design

```css
@media (max-width: 700px) {
    .container {
        padding: 20px 15px;
    }
    
    h1 {
        font-size: 1.6rem;
    }

    .controls-grid {
        grid-template-columns: 1fr;
    }
}
```

## File Template

A minimal template for new demos:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[Principle] — De Principiis</title>
    <style>
        /* Paste the CSS variables and base styles from ants.html */
    </style>
</head>
<body>
    <button class="theme-toggle" onclick="toggleTheme()">
        <span id="theme-icon">☀️</span> <span id="theme-label">Light</span>
    </button>

    <div class="container">
        <header>
            <div class="breadcrumb">
                <a href="index.html">De Principiis</a> → [Principle]
            </div>
            <h1>[Principle]</h1>
            <p class="subtitle">[Tagline]</p>
        </header>

        <main class="main-content">
            <p class="description">[Description]</p>
            
            <!-- Simulation goes here -->

            <div class="controls">
                <div class="controls-header">Controls</div>
                <!-- Controls go here -->
            </div>
        </main>

        <footer>
            <p><a href="index.html">← Back to De Principiis</a></p>
        </footer>
    </div>

    <script>
        // Theme handling
        function initTheme() { /* ... */ }
        function toggleTheme() { /* ... */ }
        function updateThemeUI(theme) { /* ... */ }
        initTheme();

        // Simulation code
    </script>
</body>
</html>
```

## Checklist for New Demos

- [ ] Include CSS custom properties for theming
- [ ] Add theme toggle button
- [ ] Add breadcrumb navigation
- [ ] Add back link in footer
- [ ] Use Georgia serif font
- [ ] Test in both light and dark modes
- [ ] Test responsiveness on mobile
- [ ] Keep all code self-contained (no external dependencies)
