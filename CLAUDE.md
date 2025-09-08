# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the Awesome-CV LaTeX template repository - a clean, customizable LaTeX template for creating CVs, résumés, and cover letters. The template uses XeLaTeX for compilation due to its use of custom fonts and the fontspec package.

## Build Commands

### Compile a Single Document
```bash
# Must use XeLaTeX (NOT pdflatex) because the template uses fontspec
xelatex <filename>.tex

# Example for the main file
xelatex song.tex
```

### Build Examples
```bash
# Build all example documents (resume, CV, cover letter)
make examples

# Build individual examples
make resume.pdf
make cv.pdf
make coverletter.pdf

# Clean build artifacts in examples directory
make clean
```

### Docker Build (if dependencies not installed)
```bash
docker run --rm --user $(id -u):$(id -g) -i -w "/doc" -v "$PWD":/doc texlive/texlive:latest make
```

## Architecture

### Core Components

1. **awesome-cv.cls** - The main class file that defines the entire template structure and styling. Key features:
   - Requires XeLaTeX or LuaLaTeX (uses fontspec package)
   - Configured for Korean font support (Apple SD Gothic Neo on macOS)
   - Uses FontAwesome5 for icons
   - Provides custom commands for CV sections and formatting

2. **Document Types**:
   - **resume.tex** - One or two-page résumé format
   - **cv.tex** - Multi-page curriculum vitae format  
   - **coverletter.tex** - Cover letter with optional sections
   - Each main document imports section files from subdirectories (e.g., `resume/education.tex`)

3. **Section Structure**:
   - Documents are modular - each section (education, experience, skills, etc.) is in a separate `.tex` file
   - Sections are imported using `\input{section_name}` commands
   - This allows easy reordering and reuse of sections between CV and résumé

### Key LaTeX Commands Defined by the Class

- Personal information: `\name{}`, `\position{}`, `\address{}`, `\mobile{}`, `\email{}`, `\github{}`, `\linkedin{}`
- Section formatting: `\cvsection{}`, `\cvsubsection{}`
- Content entries: `\cventry{}`, `\cvsubentry{}`, `\cvhonor{}`, `\cvskill{}`
- Letter components: `\lettertitle{}`, `\letteropening{}`, `\letterclosing{}`, `\letterenclosure{}`

## Common Issues and Solutions

1. **Compilation Error: "Fatal Package fontspec Error"**
   - Solution: Use `xelatex` instead of `pdflatex`

2. **Font Warnings**: The template may show warnings about missing font shapes (italic/slanted variants). These are typically harmless - the system will substitute available variants.

3. **Korean/CJK Text Support**: The current configuration uses Apple SD Gothic Neo font for Korean text on macOS. For other systems, you may need to modify the font settings in awesome-cv.cls lines 83-85.

## File Organization

```
.
├── awesome-cv.cls          # Main template class file
├── examples/              
│   ├── resume.tex         # Resume main file
│   ├── cv.tex            # CV main file
│   ├── coverletter.tex   # Cover letter main file
│   ├── resume/           # Resume section files
│   │   ├── education.tex
│   │   ├── experience.tex
│   │   └── ...
│   └── cv/               # CV section files
│       ├── education.tex
│       ├── experience.tex
│       └── ...
├── Makefile              # Build automation
└── song.tex              # User's custom CV/resume
```