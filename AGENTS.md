# AGENTS.md

This file contains conventions and guidelines for agentic coding tools working in this Jekyll CV repository.

## Project Overview

This is a Jekyll-based static site for a personal CV/resume website. The site generates HTML from Markdown templates and is hosted on GitHub Pages.

## Build and Development Commands

### Local Development

- `jekyll serve` - Start local development server (default: http://localhost:4000)
- `jekyll build` - Build the static site to `_site/` directory
- `jekyll clean` - Clean the build directory

### Testing

No automated tests are currently configured. Manual testing involves:
1. Run `jekyll serve`
2. Open http://localhost:4000 in browser
3. Verify layout and content rendering
4. Check print preview for CV formatting (Ctrl/Cmd + P)

### Linting/Formatting
No automated linting or formatting tools are currently configured for this project.

---

## File Structure

```
.
├── _config.yml          # Jekyll configuration (markdown engine, theme)
├── _layouts/            # HTML templates
│   └── cv.html         # Main CV layout
├── _includes/          # Markdown partials (reusable sections)
│   ├── header.md       # Name, contact info
│   ├── specialities.md # Professional summary
│   ├── skills.md       # Skills section
│   ├── exp.md          # Work experience
│   ├── exp_ai_generated.md # AI-generated work experience variant
│   ├── edu.md          # Education
│   └── interests.md    # Personal interests
├── media/              # CSS stylesheets
│   ├── davewhipp-screen.css  # Screen styling
│   └── davewhipp-print.css   # Print styling
├── index.md            # Main CV page
└── hr.md               # HR-specific CV variant
```

---

## Code Style Guidelines

### Front Matter (YAML)
All markdown files must begin with YAML front matter:
```yaml
---
layout: cv
title: Anton Panteleev
---
```

### Markdown Content

#### Sections and Headers
- Use `##` for major section headings (Skills, Work Experience, Education)
- Use `###` for subsections
- No `#` header needed in include files (handled by main template)

#### Dates and Timelines
Format dates as: `YYYY.MON` (e.g., `2025.SEP`, `2023.OCT`)
Range format: `START-END` (e.g., `2021.NOV-2023.AUG`)
Use backticks around date ranges: `` `2021.NOV-2023.AUG` ``

#### Company and Role Formatting
- Company names: double underscores for bold: `__Marketplacer__`
- Job title: plain text after company
- Location: format as `City, Country code` (e.g., `Melbourne, AUS`)
- Full format: `` `2025.SEP-2025.DEC`\n__Marketplacer__, Software Engineer. Melbourne, AUS``

#### Bullet Points
- Use standard markdown `-` for bullet points
- Start each bullet with action verbs: Built, Developed, Implemented, Improved
- Keep bullets concise but informative
- Use technical terms and technologies as written: Ruby on Rails, AWS, PostgreSQL
- Comments can use HTML-style: `<!-- comment -->`

#### Links and Contact Info
- Format: `[label](url)`
- Email: `[email: address@domain.com](mailto:address@domain.com)`
- Social links: `[Platform: username](url)`

#### Code/Inline Formatting
- Use backticks for inline code: `jekyll serve`
- Use backticks for date ranges as shown above

### Liquid Template Syntax

#### Including Partials
```
{% include filename.md %}
```

#### Outputting Page Variables
```
{{ content }}
{{ page.title }}
{{ site.style }}
```

### HTML Layouts

#### Doctype and Structure
```html
<!doctype html>
<html>
<head>
  <meta charset=utf-8 />
  <title> {% if page.title %} {{ page.title }} | {% endif %} CV</title>
  <link href="media/{{ site.style }}-screen.css" type="text/css" rel="stylesheet" media="screen">
  <link href="media/{{ site.style }}-print.css" type="text/css" rel="stylesheet" media="print">
</head>
<body>
  <div id="main">
    <div id="content">
    {{ content }}
    </div>
  </div>
</body>
</html>
```

### CSS Guidelines

#### Reset and Base
- Uses Meyer CSS reset (public domain)
- Primary fonts: Avenir, Verdana for body; Cousine for headers
- Screen width: centered at 50% for screens > 1200px

#### Typography
- Body: 80% font size, 1.5em line height
- Headers: weight 400 (not bold)
- H1: 3em, left-aligned
- H2: 1.1em, right-aligned, color #bc412b
- H3: 1em, right-aligned

#### Layout Positioning
- Content area: left 25%, width 75% for paragraphs and lists
- Headers: width 80%, specific positioning via left/top offsets
- No bullet points visible (commented out), but indentation preserved

#### Link Styling
- Default: inherit color
- Hover: color #39f (blue)

---

## Naming Conventions

### Files and Directories
- All lowercase with underscores: `_includes`, `_layouts`
- Markdown files: `.md` extension
- CSS files: `{theme}-{screen|print}.css` format

### Content Naming
- Include files: single word, lowercase: `skills.md`, `exp.md`
- Page files: descriptive names: `index.md`, `hr.md`
- CSS themes: lowercase: `davewhipp`, `kjhealy`

---

## Best Practices

### Content Updates
- Update both `exp.md` and `exp_ai_generated.md` when adding experience
- Keep chronological order (most recent first)
- Maintain consistent formatting across sections
- Use HTML comments for alternate content or notes, not for production text

### Styling Changes
- Test both screen and print views when modifying CSS
- Both davewhipp and kjhealy themes exist - update both if changing structure
- Maintain responsive behavior for mobile devices

### Jekyll Configuration
- `style` in `_config.yml` controls which CSS theme is used
- `markdown: kramdown` is the current markdown processor
- No additional plugins or custom configurations

---

## Git Workflow

### Ignored Files
- `_site/` - Generated site files
- `.sass-cache/` - SASS compilation cache
- `.obsidian/` - Obsidian notes directory

### Committing
- Commit markdown content and CSS changes
- Do not commit `_site/` directory
- Test locally before pushing to verify rendering

---

## Technology Stack

- **Static Site Generator**: Jekyll (Ruby gem)
- **Markdown Processor**: Kramdown
- **Styling**: Pure CSS (no preprocessor)
- **Hosting**: GitHub Pages
- **Deployment**: Git push to repository

---

## Common Tasks

### Add New Work Experience
1. Edit `_includes/exp.md` or `_includes/exp_ai_generated.md`
2. Add new entry at top of Work Experience section
3. Follow date/role/company/location format
4. Add bullet points with accomplishments
5. Test locally with `jekyll serve`

### Add New Skill Category
1. Edit `_includes/skills.md`
2. Add category with bold/italic as needed
3. List skills with proper separators
4. Maintain consistent formatting with existing entries

### Switch CSS Theme
1. Edit `_config.yml`
2. Change `style: davewhipp` to `style: kjhealy` (or vice versa)
3. Run `jekyll serve` to verify
