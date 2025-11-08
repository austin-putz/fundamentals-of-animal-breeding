# Animal Breeding and Genetics Textbook

**A Practical Introduction for Undergraduate Students**

This repository contains the source files for an undergraduate textbook on Animal Breeding and Genetics, designed as the first course in animal breeding and genetics for students in animal science programs.

## Overview

This textbook bridges theoretical concepts with practical applications in modern livestock breeding, emphasizing:

- **Industry relevance**: Real-world examples from commercial breeding programs
- **Quantitative skills**: Building comfort with equations, heritability, genetic correlations, and selection theory
- **Computational literacy**: R programming for genetic calculations and data analysis
- **Species diversity**: Examples across swine, poultry, dairy, beef, horses, and small ruminants
- **Modern genomics**: Introduction to genomic selection at an appropriate undergraduate level

## Prerequisites

To build and render this book locally, you'll need:

1. **R** (version 4.0.0 or higher)
   - Download from [CRAN](https://cran.r-project.org/)

2. **Quarto** (version 1.3.0 or higher)
   - Download from [quarto.org](https://quarto.org/docs/get-started/)

3. **RStudio** (recommended but optional)
   - Download from [posit.co](https://posit.co/download/rstudio-desktop/)

4. **R Packages** (these will be loaded as needed in chapters):
   - tidyverse
   - ggplot2
   - pedigree
   - AGHmatrix
   - nadiv
   - Additional packages as specified in individual chapters

## Quick Start

### 1. Clone or Download the Repository

```bash
git clone <repository-url>
cd AnimalBreedingUndergrad
```

Or download and extract the ZIP file if you don't use Git.

### 2. Open the Project

If using RStudio:
- Open the `AnimalBreedingUndergrad.Rproj` file (if present), or
- Navigate to File → Open Project and select the project folder

If using command line:
- Navigate to the project directory in your terminal

### 3. Render the Book

**Option A: Using RStudio**
- Open the Terminal tab in RStudio
- Run: `quarto render`

**Option B: Using Command Line**
```bash
quarto render
```

**Option C: Using R Console**
```r
quarto::quarto_render()
```

This will build the entire book and output HTML files to the `docs/` directory.

### 4. Preview the Book

**Option A: Live Preview (Recommended for Development)**
```bash
quarto preview
```

This will:
- Render the book
- Start a local web server
- Open the book in your default browser
- Automatically refresh when you make changes to `.qmd` files

**Option B: Open the Rendered Book**

After rendering, open `docs/index.html` in your web browser:
- **Mac**: `open docs/index.html`
- **Windows**: `start docs/index.html`
- **Linux**: `xdg-open docs/index.html`

Or simply navigate to the `docs/` folder and double-click `index.html`.

## Project Structure

```
AnimalBreedingUndergrad/
├── _quarto.yml           # Quarto configuration file
├── index.qmd             # Book homepage/preface
├── chapters/             # Book chapters
│   ├── 01-introduction.qmd
│   ├── 02-selection-basics.qmd
│   ├── 03-genetic-model.qmd
│   ├── 04-quantitative-traits.qmd
│   ├── 05-heritability-repeatability.qmd
│   ├── 06-breeders-equation.qmd
│   ├── 07-breeding-values.qmd
│   ├── 08-genetic-correlations.qmd
│   ├── 09-selection-index.qmd
│   ├── 10-mating-strategies.qmd
│   ├── 11-crossbreeding.qmd
│   ├── 12-genomics-intro.qmd
│   ├── 13-genomic-selection.qmd
│   └── 14-practical-skills.qmd
├── appendices/           # Appendix materials
│   ├── datasets.qmd
│   ├── r-resources.qmd
│   └── glossary.qmd
├── data/                 # Datasets used in examples
├── images/               # Images and figures
├── R/                    # R functions and scripts
├── docs/                 # Rendered HTML output (generated)
├── custom.scss           # Custom styling (SCSS)
├── styles.css            # Additional CSS styles
├── references.bib        # Bibliography file
├── CLAUDE.md             # Development guide and instructions
└── README.md             # This file
```

## Development Workflow

### Editing Chapters

1. Open any `.qmd` file in the `chapters/` directory
2. Edit the content using Quarto markdown syntax
3. Add R code chunks as needed:

````markdown
```{r}
# Your R code here
```
````

4. Save the file
5. If using `quarto preview`, changes will automatically refresh in the browser
6. Otherwise, re-render the book with `quarto render`

### Adding New Chapters

1. Create a new `.qmd` file in the `chapters/` directory
2. Add the chapter to `_quarto.yml` under the appropriate section:

```yaml
chapters:
  - chapters/your-new-chapter.qmd
```

3. Render the book to see your changes

### Working with Data

- Place datasets in the `data/` directory
- Use relative paths in R code: `read.csv("data/your-dataset.csv")`
- Document datasets in `appendices/datasets.qmd`

### Adding Images

- Place images in the `images/` directory
- Reference in markdown: `![Caption](images/your-image.png)`

## Rendering Options

### Render Entire Book
```bash
quarto render
```

### Render a Single Chapter
```bash
quarto render chapters/01-introduction.qmd
```

### Clean Build (Remove Cache)
```bash
quarto render --clean
```

### Render to Different Formats

The default output is HTML. To render to other formats, modify `_quarto.yml` or use:

```bash
# PDF (requires LaTeX)
quarto render --to pdf

# Word document
quarto render --to docx

# EPUB
quarto render --to epub
```

## Troubleshooting

### Quarto Not Found
If you get "quarto: command not found":
- Ensure Quarto is installed
- Restart your terminal/RStudio after installation
- Check installation: `quarto --version`

### R Package Errors
If you encounter missing package errors:
```r
install.packages("package-name")
```

### Render Errors
If rendering fails:
1. Check the error message for specific file/line
2. Try rendering just that chapter: `quarto render chapters/XX-chapter.qmd`
3. Clear cache: `quarto render --clean`
4. Check R code chunks for errors

### Port Already in Use (Preview)
If `quarto preview` fails because port is in use:
```bash
quarto preview --port 4321
```

## Book Content

### Part I: Foundations of Animal Breeding
- Chapter 1: Introduction to Animal Breeding
- Chapter 2: Selection Basics
- Chapter 3: Basic Genetic Model (y = A + E)
- Chapter 4: Quantitative vs. Simply Inherited Traits

### Part II: Genetic Parameters
- Chapter 5: Heritability and Repeatability
- Chapter 6: Breeder's Equation and Selection Response

### Part III: Selection Methods
- Chapter 7: Estimating Breeding Values
- Chapter 8: Genetic Correlations and Correlated Response
- Chapter 9: Multiple Trait Selection and Selection Index

### Part IV: Mating Systems and Crossbreeding
- Chapter 10: Mating Strategies and Optimum Contribution Selection
- Chapter 11: Crossbreeding and Hybrid Vigor

### Part V: Genomic Tools
- Chapter 12: Introduction to Genomics
- Chapter 13: Genomic Selection

### Part VI: Practical Applications
- Chapter 14: Practical Animal Breeding and Data Skills

## Additional Resources

- **CLAUDE.md**: Comprehensive development guide with writing guidelines, technical standards, and chapter-by-chapter instructions
- **Appendices**: Datasets documentation, R resources, and glossary
- **References**: Bibliography in BibTeX format (`references.bib`)

## Target Audience

**Primary audience**: Undergraduate juniors/seniors taking their first animal breeding course

**Prerequisites**:
- Introductory genetics (Mendelian genetics, basic molecular biology)
- Basic statistics (mean, variance, correlation, simple linear regression)
- Introductory R programming (or willingness to learn alongside the course)

## Author

Austin Putz

## License

[Add license information here]

## Questions or Issues?

[Add contact information or issue reporting guidelines here]

---

**Happy Learning and Teaching!**
