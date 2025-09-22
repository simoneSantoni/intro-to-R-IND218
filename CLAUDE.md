# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview
This repository contains materials for an introductory course on R for analytics students (IND215). It includes a Quarto-based website with course materials and focuses on R fundamentals and the tidyverse ecosystem.

## Project Architecture

### Website Structure
- `/website/` - Main Quarto website directory
- `website/_quarto.yml` - Primary Quarto configuration with site structure, theming, and R kernel setup
- `website/index.qmd` - Homepage featuring comprehensive R learning journey and humorous timeline
- `website/course/` - Course administrative content (syllabus, schedule, team, support)
- `website/modules/` - Six-module course structure with hierarchical content organization

### Content Organization
The course follows a progressive six-module structure:

1. **Module 1**: Getting Started (R/RStudio setup, interface, projects)
2. **Module 2**: R Fundamentals (objects, data types, vectors, data frames, functions)
3. **Module 3**: Tidyverse Introduction (readr, dplyr basics, tidyr principles)
4. **Module 4**: Data Types in Tidyverse (strings, factors, dates, categorical data)
5. **Module 5**: Data Wrangling with dplyr (filtering, grouping, joins, advanced manipulation)
6. **Module 6**: Organizing Tabular Data with tidyr (pivoting, reshaping, nested data)

### Technical Configuration
- **R Kernel**: Uses "ir" kernel for R code execution in Jupyter/Quarto
- **Theming**: Cosmo-based responsive design with custom light/dark themes
- **Typography**: Atkinson Hyperlegible font for accessibility
- **Code Handling**: Auto-freeze execution, syntax highlighting, copy functionality

## Key Commands

### Development Workflow
- `quarto preview website` - Start local development server with live reload
- `quarto render website` - Build complete static site to `_site/` directory
- `quarto publish` - Deploy to hosting platform (if configured)

### Content Management
- `quarto create article filename.qmd` - Create new content file with template
- R code execution happens automatically during render via R kernel

## Website Features

### Navigation & UI
- Docked sidebar with search functionality and GitHub integration
- Responsive navigation with hierarchical module structure
- Edit page links and issue reporting directly to GitHub repository
- Custom theme switcher for light/dark modes

### R Integration
- Live R code execution in `.qmd` files via Jupyter R kernel
- Code copying, syntax highlighting, and overflow handling
- Freeze capability to cache expensive computations
- Support for R Markdown-style code chunks and outputs

### Course Content Philosophy
- Hands-on learning with real datasets and practical exercises
- Humorous approach to R learning (see comprehensive timeline in `index.qmd`)
- Industry-relevant examples emphasizing tidyverse best practices
- Statistical computing foundation with modern data science workflows

## Development Notes
- Website deploys to GitHub Pages at https://simonesantoni.github.io/intro-to-R-IND215
- Content emphasizes tidyverse ecosystem over base R where appropriate
- Custom SCSS themes (`theme.scss`, `theme-dark.scss`) extend Cosmo bootstrap theme
- R kernel configuration assumes `ind215` named kernel for consistent environment