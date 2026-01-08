# PDF Export Instructions

This document provides step-by-step instructions for exporting the Okta technical documentation to PDF format.

## Prerequisites

- Base page: `00-base/okta-docs-base-page-v1.md`
- All referenced sub-pages and images

## Option A: Using VS Code / Markdown PDF Extension

### Step 1: Install Extension
1. Open VS Code
2. Go to Extensions (Ctrl+Shift+X)
3. Search for "Markdown PDF" extension
4. Install the extension

### Step 2: Configure Export Settings
1. Open VS Code Settings (Ctrl+,)
2. Search for "markdown-pdf"
3. Configure the following settings:
   - Enable "markdown-pdf.includeDefaultStyles"
   - Set "markdown-pdf.outputDirectory" to desired output location
   - Configure "markdown-pdf.styles" if custom CSS is needed

### Step 3: Export Base Page
1. Open `docs/00-base/okta-docs-base-page-v1.md`
2. Right-click in the editor
3. Select "Markdown PDF: Export (pdf)"
4. The PDF will be generated with all linked sub-pages and images

### Step 4: Verify Export
1. Check the output directory for the generated PDF
2. Verify all pages and images are included
3. Review formatting and layout

---

## Option B: Using Pandoc

### Step 1: Install Pandoc
1. Download Pandoc from: https://pandoc.org/installing.html
2. Install Pandoc on your system
3. Verify installation: `pandoc --version`

### Step 2: Prepare Markdown Files
1. Ensure all markdown files are in the correct directory structure
2. Verify all image paths are correct relative paths
3. Check that all internal links are valid

### Step 3: Export Base Page
1. Navigate to the docs directory
2. Run the following command:
   ```
   pandoc 00-base/okta-docs-base-page-v1.md -o okta-docs-export.pdf --pdf-engine=xelatex --toc --toc-depth=3
   ```

### Step 4: Include Sub-pages (Advanced)
1. Create a master markdown file that includes all sub-pages
2. Use Pandoc's include functionality or concatenate files
3. Run Pandoc with the master file

### Step 5: Configure Images
1. Ensure image paths are relative to the markdown file location
2. Pandoc will automatically include images referenced in markdown
3. For custom image sizing, use HTML img tags in markdown

### Step 6: Customize Output
1. Create a custom LaTeX template if needed
2. Use Pandoc filters for advanced formatting
3. Configure PDF metadata using YAML front matter

---

## Troubleshooting

### Common Issues

1. **Images not appearing**: Check image paths are relative and files exist
2. **Links broken**: Verify all internal markdown links use correct relative paths
3. **Formatting issues**: Review markdown syntax and Pandoc/extension settings
4. **Missing pages**: Ensure all sub-pages are properly linked from the base page

### Tips

- Test export with a single page first before exporting the entire documentation set
- Keep image file sizes reasonable for faster PDF generation
- Use consistent heading levels for better table of contents generation
- Review the generated PDF for any formatting issues before finalizing

