# Style Guide - Documentation Standards

## Document Metadata

- **Version:** 1.0
- **Status:** Draft
- **Owner:** Technical Documentation Team
- **Last Updated:** 2026-01-08
- **Related ADRs:** N/A

---

## Table of Contents

- [Overview](#overview)
- [Color Palette](#color-palette)
- [Icons](#icons)
- [Typography](#typography)
- [Spacing and Layout](#spacing-and-layout)
- [Markdown Standards](#markdown-standards)
- [Code Formatting](#code-formatting)
- [Images and Assets](#images-and-assets)
- [Accessibility](#accessibility)

---

## Overview

This style guide defines the visual and formatting standards for Okta technical documentation. All documentation should adhere to these guidelines to ensure consistency, readability, and professional presentation across all documents.

### Purpose

- Establish consistent visual identity across all documentation
- Ensure accessibility and readability
- Provide clear guidelines for contributors
- Maintain professional appearance

### Scope

This guide applies to:
- All markdown documentation files
- Generated PDF exports
- Embedded images and diagrams
- Code examples and snippets
- Tables and data visualizations

---

## Color Palette

### Primary Colors

The Okta documentation uses the following color palette:

#### Brand Colors

- **Okta Blue (Primary):** `#007DC1`
  - Usage: Headers, links, primary actions, brand elements
  - Hex: `#007DC1`
  - RGB: `rgb(0, 125, 193)`

- **Okta Dark Blue:** `#00297A`
  - Usage: Dark backgrounds, emphasis, secondary elements
  - Hex: `#00297A`
  - RGB: `rgb(0, 41, 122)`

#### Semantic Colors

- **Success/Green:** `#00A86B`
  - Usage: Success messages, positive indicators, completed states
  - Hex: `#00A86B`
  - RGB: `rgb(0, 168, 107)`

- **Warning/Orange:** `#FF6B35`
  - Usage: Warnings, caution messages, important notices
  - Hex: `#FF6B35`
  - RGB: `rgb(255, 107, 53)`

- **Error/Red:** `#E53E3E`
  - Usage: Error messages, critical alerts, destructive actions
  - Hex: `#E53E3E`
  - RGB: `rgb(229, 62, 62)`

- **Info/Blue:** `#3182CE`
  - Usage: Informational messages, tips, general notices
  - Hex: `#3182CE`
  - RGB: `rgb(49, 130, 206)`

#### Neutral Colors

- **Text Primary:** `#1A202C`
  - Usage: Main body text, headings
  - Hex: `#1A202C`
  - RGB: `rgb(26, 32, 44)`

- **Text Secondary:** `#4A5568`
  - Usage: Secondary text, captions, metadata
  - Hex: `#4A5568`
  - RGB: `rgb(74, 85, 104)`

- **Border/Divider:** `#E2E8F0`
  - Usage: Borders, dividers, separators
  - Hex: `#E2E8F0`
  - RGB: `rgb(226, 232, 240)`

- **Background:** `#FFFFFF`
  - Usage: Document background
  - Hex: `#FFFFFF`
  - RGB: `rgb(255, 255, 255)`

- **Background Secondary:** `#F7FAFC`
  - Usage: Code blocks, highlighted sections, alternate rows
  - Hex: `#F7FAFC`
  - RGB: `rgb(247, 250, 252)`

### Color Usage Guidelines

1. **Consistency:** Use the same color for the same purpose throughout all documentation
2. **Contrast:** Ensure sufficient contrast ratios for accessibility (WCAG AA minimum)
3. **Meaning:** Use semantic colors appropriately (red for errors, green for success)
4. **Sparingly:** Avoid overuse of colors; maintain professional appearance

---

## Icons

### Icon Library

The Okta documentation uses **Font Awesome** icons for consistency. When icons are needed in documentation, use Font Awesome icon names and classes.

#### Recommended Icon Sets

- **Font Awesome 6.x** (Free version)
  - Website: https://fontawesome.com/
  - CDN: Available via Font Awesome CDN
  - License: Free for documentation use

### Common Icons

Use the following icons for standard documentation elements:

#### Status and State Icons

- **Success/Check:** `fa-check-circle` or `fa-check`
- **Error/Warning:** `fa-exclamation-circle` or `fa-exclamation-triangle`
- **Info:** `fa-info-circle`
- **Question:** `fa-question-circle`

#### Navigation Icons

- **Home:** `fa-home`
- **Documentation:** `fa-book` or `fa-file-alt`
- **Link/External:** `fa-external-link-alt`
- **Arrow Right:** `fa-arrow-right`
- **Arrow Left:** `fa-arrow-left`

#### Technology Icons

- **Code/Development:** `fa-code`
- **Database:** `fa-database`
- **Server:** `fa-server`
- **Cloud:** `fa-cloud`
- **API:** `fa-plug`
- **Security:** `fa-shield-alt` or `fa-lock`
- **Git/GitHub:** `fa-github`

#### Process Icons

- **Workflow:** `fa-project-diagram` or `fa-sitemap`
- **Deployment:** `fa-rocket`
- **Testing:** `fa-flask` or `fa-vial`
- **Monitoring:** `fa-chart-line` or `fa-eye`

### Icon Usage Guidelines

1. **Consistency:** Use the same icon for the same concept across all documents
2. **Size:** Icons should be appropriately sized relative to text (typically 1em or 1.2em)
3. **Color:** Icons should use colors from the color palette
4. **Accessibility:** Always provide alternative text or aria-labels for icons
5. **Sparingly:** Use icons to enhance understanding, not as decoration

### Icon Implementation

For HTML/Markdown with HTML support:
```html
<i class="fas fa-check-circle" style="color: #00A86B;"></i> Success
```

For pure Markdown:
- Use Unicode symbols sparingly: ✓ ✗ ⚠ ℹ
- Or describe icons in text: [Success Icon] or (✓)

---

## Typography

### Font Families

#### Primary Font
- **Sans-serif:** System default (Arial, Helvetica, sans-serif)
  - Usage: Body text, headings, UI elements
  - Fallback: Arial, Helvetica, sans-serif

#### Monospace Font
- **Code Font:** 'Courier New', Courier, monospace
  - Usage: Code blocks, inline code, file paths, commands
  - Alternative: 'Consolas', 'Monaco', monospace

### Font Sizes

#### Headings Hierarchy

- **H1 (Page Title):** 32px / 2em
  - Usage: Main page title
  - Weight: Bold (700)

- **H2 (Section):** 24px / 1.5em
  - Usage: Major sections
  - Weight: Bold (700)

- **H3 (Subsection):** 20px / 1.25em
  - Usage: Subsections
  - Weight: Semi-bold (600)

- **H4 (Sub-subsection):** 18px / 1.125em
  - Usage: Minor subsections
  - Weight: Semi-bold (600)

- **H5 (Minor heading):** 16px / 1em
  - Usage: Minor headings
  - Weight: Medium (500)

- **H6 (Smallest heading):** 14px / 0.875em
  - Usage: Smallest headings
  - Weight: Medium (500)

#### Body Text

- **Body Text:** 16px / 1em
  - Usage: Paragraphs, lists, general content
  - Line height: 1.6
  - Weight: Regular (400)

- **Small Text:** 14px / 0.875em
  - Usage: Captions, metadata, footnotes
  - Line height: 1.5
  - Weight: Regular (400)

#### Code Text

- **Inline Code:** 14px / 0.875em
  - Usage: Inline code snippets, variables, file names
  - Font: Monospace

- **Code Blocks:** 14px / 0.875em
  - Usage: Code examples, scripts
  - Font: Monospace
  - Line height: 1.5

### Typography Guidelines

1. **Hierarchy:** Maintain clear heading hierarchy (H1 → H2 → H3, etc.)
2. **Consistency:** Use the same font sizes for the same element types
3. **Readability:** Ensure sufficient line height for readability
4. **Emphasis:** Use **bold** for strong emphasis, *italic* for subtle emphasis
5. **Code:** Always use monospace font for code-related content

---

## Spacing and Layout

### Spacing Standards

#### Vertical Spacing

- **Between sections (H2):** 48px / 3em
- **Between subsections (H3):** 32px / 2em
- **Between paragraphs:** 16px / 1em
- **Between list items:** 8px / 0.5em
- **Between table rows:** 12px / 0.75em

#### Horizontal Spacing

- **Page margins:** 40px / 2.5em (left/right)
- **Content width:** Maximum 1200px
- **Code block padding:** 16px / 1em
- **Table cell padding:** 12px / 0.75em

### Layout Guidelines

1. **Width:** Keep content width reasonable for readability (max 1200px)
2. **Alignment:** Left-align text (except for specific cases like code)
3. **Whitespace:** Use adequate whitespace to separate sections
4. **Consistency:** Maintain consistent spacing throughout documents

---

## Markdown Standards

### Document Structure

All documentation files should follow this structure:

1. **Title (H1)**
2. **Document Metadata** (as specified in template)
3. **Table of Contents**
4. **Main Content** (H2 sections)
5. **Images Section** (if applicable)
6. **Sub-pages Section** (if applicable)

### Markdown Formatting

#### Headers
- Use `#` for H1 (page title only)
- Use `##` for H2 (major sections)
- Use `###` for H3 (subsections)
- Use `####` for H4 and below as needed

#### Lists
- Use `-` for unordered lists
- Use `1.` for ordered lists
- Indent nested lists with 2 spaces

#### Emphasis
- Use `**bold**` for strong emphasis
- Use `*italic*` for subtle emphasis
- Use `` `code` `` for inline code

#### Links
- Format: `[Link Text](path/to/file.md)`
- Use relative paths for internal links
- Use descriptive link text

#### Tables
- Use pipe (`|`) delimiters
- Include header row with separator row
- Align columns as needed

### Markdown Best Practices

1. **Consistency:** Follow the same formatting patterns throughout
2. **Clarity:** Use clear, descriptive headings
3. **Links:** Keep link text descriptive and meaningful
4. **Lists:** Use lists for multiple related items
5. **Tables:** Use tables for structured data

---

## Code Formatting

### Code Block Standards

#### Language Specification
Always specify the language for code blocks:

````markdown
```php
// PHP code example
```

```javascript
// JavaScript code example
```

```bash
# Shell command
```
````

#### Supported Languages
- PHP (Laravel)
- JavaScript/TypeScript
- Bash/Shell
- SQL
- JSON
- YAML
- Markdown
- HTML/CSS

### Inline Code

Use backticks for:
- Variable names: `$userId`
- Function names: `getUser()`
- File paths: `app/Models/User.php`
- Commands: `php artisan migrate`
- Configuration keys: `config('app.name')`

### Code Block Styling

- Background: `#F7FAFC` (light gray)
- Border: `#E2E8F0` (border color)
- Padding: 16px
- Font: Monospace, 14px
- Line numbers: Optional, use when helpful

### Code Formatting Guidelines

1. **Syntax Highlighting:** Always specify language for syntax highlighting
2. **Readability:** Format code for readability (proper indentation)
3. **Completeness:** Include complete, working examples when possible
4. **Comments:** Add comments to explain complex code
5. **Context:** Provide context for code examples

---

## Images and Assets

### Image Standards

#### Formats
- **Diagrams/Charts:** PNG (for diagrams with text) or SVG (for scalable graphics)
- **Screenshots:** PNG or JPG
- **Icons:** SVG (preferred) or PNG

#### Dimensions
- **Maximum width:** 1200px (for full-width images)
- **Standard width:** 800px (for most images)
- **Thumbnail width:** 400px (for smaller images)

#### Quality
- **Resolution:** Minimum 72 DPI for web, 300 DPI for PDF export
- **Compression:** Optimize images for file size while maintaining quality
- **File size:** Keep images under 500KB when possible

### Image Organization

Store images in: `assets/images/`

Structure:
```
assets/
  images/
    architecture/
    diagrams/
    screenshots/
    icons/
```

### Image Usage in Markdown

```markdown
![Alt text describing the image](assets/images/filename.png)
```

### Image Guidelines

1. **Alt Text:** Always provide descriptive alt text
2. **Naming:** Use descriptive, lowercase filenames with hyphens
3. **Organization:** Organize images in subdirectories by category
4. **References:** Reference images in the "Images" section of documents
5. **Consistency:** Use consistent styling for diagrams (colors, fonts)

---

## Accessibility

### Color Contrast

Ensure sufficient contrast ratios:
- **Normal text:** Minimum 4.5:1 contrast ratio
- **Large text (18px+):** Minimum 3:1 contrast ratio
- **UI components:** Minimum 3:1 contrast ratio

### Text Alternatives

- **Images:** Always include descriptive alt text
- **Icons:** Provide text alternatives or aria-labels
- **Diagrams:** Include text descriptions for complex diagrams

### Document Structure

- **Headings:** Use proper heading hierarchy (H1 → H2 → H3)
- **Lists:** Use proper list markup (ul/ol)
- **Tables:** Use table headers and proper markup
- **Links:** Use descriptive link text (avoid "click here")

### Accessibility Guidelines

1. **Contrast:** Verify color contrast meets WCAG AA standards
2. **Alt Text:** Provide meaningful alt text for all images
3. **Structure:** Use semantic HTML/Markdown structure
4. **Navigation:** Ensure documents are navigable via keyboard
5. **Readability:** Write clear, concise text

---

## Images

- ![Color Palette](assets/images/style-guide-color-palette.png)
- ![Typography Examples](assets/images/style-guide-typography.png)
- ![Icon Examples](assets/images/style-guide-icons.png)

---

## Sub-pages

- [Okta Documentation Base Page](okta-docs-base-page-v0.md)
- [Engineering Handbook](../01-foundation/engineering-handbook-v0.md)
