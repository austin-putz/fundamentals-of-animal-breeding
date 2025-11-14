# Animal Breeding and Genetics Textbook Development Guide

## Book Overview

### Purpose and Goals

This textbook is designed as the **first course in animal breeding and genetics** for undergraduate students in animal science programs. The book bridges theoretical concepts with practical applications in modern livestock breeding, emphasizing:

- **Industry relevance**: Real-world examples from commercial breeding programs
- **Quantitative skills**: Building comfort with equations, heritability, genetic correlations, and selection theory
- **Computational literacy**: R programming for genetic calculations and data analysis
- **Species diversity**: Comprehensive coverage of swine, poultry, dairy, beef, sheep, camelidae, aquaculture, and companion animals
- **Modern genomics**: Introduction to genomic selection at an appropriate undergraduate level
- **Species-specific applications**: Dedicated chapters exploring breeding programs unique to each species
- **Precision technologies**: Introduction to precision livestock farming and automated phenotyping

### Target Audience

**Primary audience**: Undergraduate juniors/seniors taking their first animal breeding course

**Prerequisites**:
- Introductory genetics (Mendelian genetics, basic molecular biology)
- Basic statistics (mean, variance, correlation, simple linear regression)
- Introductory R programming (or willingness to learn alongside the course)

**Learning outcomes**: By completion, students should be able to:
1. Understand how commercial breeding companies generate value
2. Calculate and interpret heritability, genetic correlations, and response to selection
3. Understand breeding value estimation and BLUP concepts
4. Design mating strategies including crossbreeding systems
5. Explain genomic selection and its impact on genetic improvement
6. Apply R to perform genetic calculations and data management tasks
7. Describe species-specific breeding programs and their unique challenges
8. Understand how precision livestock farming technologies enable novel phenotyping
9. Apply breeding principles to diverse species from livestock to companion animals

---

## Writing Guidelines

### Tone and Voice

- **Conversational but professional**: Approachable for undergraduates, not overly technical
- **Encouraging**: Build confidence with quantitative genetics (many students fear math)
- **Practical**: Connect every concept to real breeding decisions
- **Honest about complexity**: Don't oversimplify, but scaffold difficult concepts carefully

### Explaining Concepts

**Layered approach**:
1. **Intuition first**: Start with the "why" and practical meaning
2. **Conceptual framework**: Explain the logic before equations
3. **Mathematical details**: Present equations with careful notation
4. **Worked examples**: Step-by-step calculations with livestock data
5. **R implementation**: Show how to compute in R
6. **Interpretation**: Always return to biological/economic meaning

**Example structure**:
```
[Motivating question or industry scenario]
[Conceptual explanation in plain language]
[Mathematical formulation with clear notation]
[Numerical example with real livestock values]
[R code demonstration]
[Interpretation and industry application]
[Common mistakes to avoid]
```

### Equation Presentation

**Guidelines**:
- **Introduce all notation clearly** before using in equations
- **Build complexity gradually**: Start simple, add complexity in stages
- **Provide numerical examples** immediately after abstract equations
- **Use consistent notation** throughout the book
- **Explain the meaning** of each term in biological/genetic context

**Standard notation** (maintain consistency):
- h² = heritability (narrow-sense)
- σ²_A = additive genetic variance
- σ²_P = phenotypic variance
- r_A = genetic correlation between traits
- i = selection intensity (standardized)
- R = response to selection
- L = generation interval
- EBV = Estimated Breeding Value
- TBV = True Breeding Value
- BV = Breeding Value (general)

---

## Technical Standards

### Quarto and R Configuration

**Code visibility**:
```yaml
format:
  html:
    code-fold: false  # Hide code by default
    code-tools: true  # Allow readers to show code if desired
    code-copy: true   # Enable copy button for code blocks
```

**Code chunk options** (use at chapter level):
```r
#| echo: false        # Hide code by default
#| warning: false     # Suppress warnings
#| message: false     # Suppress messages
#| fig-width: 8
#| fig-height: 6
#| fig-align: center
```

**When to show code**:
- Show code when teaching R programming concepts (Chapter 14)
- Show key calculations when the R code directly illustrates the equation
- Otherwise, hide code but make it available via code-tools

### R Code Standards

**Style**:
- Follow tidyverse style guide
- Use meaningful variable names (not x, y, but ebv, phenotype, heritability)
- Comment generously, especially for genetic calculations
- Load all packages at the start of each chapter

**Package preferences**:
- `tidyverse` for data manipulation and plotting
- `pedigree`, `AGHmatrix`, `nadiv` for relationship matrices
- `MCMCglmm`, `brms`, or `bglr` for Bayesian models (Chapter 13)
- `lme4` for mixed models (if demonstrating BLUP concepts)
- Custom functions for educational clarity (define inline when pedagogically useful)

**Example code structure**:
```r
# Clear title describing the calculation
# Load data
data <- read_csv("data/dairy_cattle.csv")

# Calculate heritability from variance components
var_additive <- 12.5   # kg² for milk yield
var_phenotypic <- 45.0  # kg²
heritability <- var_additive / var_phenotypic

# Display result
cat("Heritability of milk yield:", round(heritability, 3))
```

### Interactive Elements

**Approach**:
- Embed Shiny apps or interactive widgets for hands-on problem-solving
- Open in separate tab/window to avoid disrupting reading flow
- Use for:
  - Selection intensity calculators
  - Breeder's equation trade-off simulators
  - Response to selection across generations
  - Index weight optimization
  - Crossbreeding system comparisons
  - Genomic accuracy estimators

**Implementation notes** (to be developed):
- Host Shiny apps separately (shinyapps.io or institutional server)
- Provide iframes or links in relevant chapter sections
- Include screenshots of the interface in the text
- Ensure apps work on mobile devices

**Placeholder format** in chapters:
```markdown
::: {.callout-note icon=false}
## Interactive Exercise

Try the [Selection Intensity Calculator](link-to-shiny-app) to explore how changing the proportion selected affects intensity and response to selection.

[Screenshot or description of the interface]
:::
```

---

## Content Guidelines

### Species Focus and Examples

**Priority species** (in order of emphasis):
1. **Swine**: Excellent for explaining litter traits, maternal effects, crossbreeding
2. **Poultry (layers and broilers)**: Short generation intervals, clear selection response examples
3. **Dairy cattle**: Classic quantitative traits, extensive data, BLUP examples
4. **Beef cattle**: Terminal vs. maternal traits, heterosis, composite breeds
5. **Horses**: Thoroughbreds for demonstrating genetic correlations, breeding value concepts
6. **Sheep/Goats**: Crossbreeding, seasonal breeding considerations

**Secondary species** (limit to 1-2 examples per book):
- **Aquaculture** (salmon, trout): Mention for genomic selection, family-based breeding
- **Companion animals** (dogs, cats): Genetic diseases, simply inherited traits (Chapter 4)

**Example distribution guidelines**:
- Each chapter should feature at least 3 different species
- Rotate species across chapters to maintain variety
- Use the same species when building on previous concepts (continuity)
- Choose species that best illustrate each concept:
  - Poultry: High intensity, short generation intervals
  - Swine: Litter size, maternal effects, three-way crosses
  - Dairy: Negative genetic correlations (milk yield vs. fertility)
  - Beef: Terminal crossbreeding, heterosis
  - Horses: Racing performance, low heritability traits

### Data and Datasets

**Creating example datasets**:
- Use realistic parameter values from literature
- Include typical ranges and variation
- Simulate from distributions that match real data characteristics
- Save datasets in `data/` directory as `.csv` files
- Document data structure in appendix

**Dataset naming**:
- Species_trait_purpose.csv
- Examples: `swine_growth_heritability.csv`, `dairy_yield_blup.csv`

**Data documentation**:
- Variable names and units
- Sample size and structure
- Source/simulation parameters
- Any data cleaning or transformations

### Industry Connections

**Company examples** (Chapter 1):
- **Swine**: Genus (Hypor, PIC), Topigs Norsvin, Genesus
- **Poultry**: Cobb-Vantress, Aviagen, Hy-Line International
- **Dairy**: Select Sires, ABS Global, Alta Genetics, CRV
- **Beef**: American Angus Association, various breed associations

**Business models**:
- Genetic improvement through selection
- Revenue from semen sales, females, intact males, embryos
- Nucleus-multiplier-commercial breeding structures
- Genomic testing services
- Consulting and technical services

**Industry structure** (Chapter 1 and throughout):
- Explain pyramid breeding structures
- Describe closed vs. open populations
- Discuss selection intensity at each level
- Connect to genetic lag and generation intervals

---

## Book Structure

The book is organized into seven major parts:

**PART 1: FUNDAMENTALS** (Chapters 1-5)
- Core concepts of animal breeding, genetics, traits, heritability, and variance components

**PART 2: SELECTION AND BREEDING STRATEGIES** (Chapters 6-9)
- Selection theory, breeding value estimation, genetic correlations, and selection indices

**PART 3: INBREEDING, MATING, AND CROSSBREEDING** (Chapters 10-11)
- Mating strategies, optimum contribution selection, inbreeding management, crossbreeding systems, and hybrid vigor

**PART 4: GENOMICS** (Chapters 12-13)
- Introduction to genomic technologies and genomic selection methods

**PART 5: PRACTICAL SKILLS** (Chapter 14)
- Data management, databases, APIs, and professional skills for animal breeding

**PART 6: SPECIES-SPECIFIC BREEDING** (Chapters 15-22)
- Deep dives into breeding programs and unique considerations for each major livestock species

**PART 7: PRECISION LIVESTOCK FARMING** (Chapters 23-25)
- Modern technologies for automated phenotyping and data collection

**APPENDICES**
- Datasets, R resources, and glossary

---

## Chapter-by-Chapter Guide

## PART 1: FUNDAMENTALS

### Chapter 1: Introduction to Animal Breeding

**Purpose**: Orient students to the field, industry context, and economic drivers

**Key topics**:
1. What is animal breeding? (genetic improvement over generations)
2. Why breeding matters (food security, efficiency, sustainability, animal welfare)
3. How genetics companies make money:
   - Selling genetics (semen, females, embryos, intact males)
   - Genomic testing services
   - Technical consulting and breeding services
4. Industry structure by species:
   - Swine: Three-tier (nucleus-multiplier-commercial)
   - Poultry: Highly integrated, 3-4 major players globally
   - Dairy: Cooperative and private AI organizations
   - Beef: Breed associations, seedstock producers
   - Horses: Registry-based, private breeders

**Learning objectives**:
- Describe how commercial breeding companies generate value
- Explain pyramid breeding structures
- Compare industry organization across livestock species
- Identify major breeding companies and their market roles

**Examples**:
- PIC/Genus swine pyramid (GP, PIC308/310, commercial crossbreds)
- Cobb-Vantress broiler breeding structure
- Holstein AI bulls and global semen sales
- Angus seedstock operations

**R demonstrations**:
- None (conceptual chapter)
- Optional: plot market share or genetic trend data

**Interactive elements**:
- None (or industry structure diagram)

**Key messages**:
- Animal breeding is a long-term, data-intensive business
- Genetic improvement creates compounding value
- Structure varies by species biology and industry organization

---

### Chapter 2: Selection Basics

**Purpose**: Introduce core concepts of traits, phenotypes, data management, and breeding objectives

**Key topics**:
1. **Traits of interest**: Production, reproduction, health, efficiency, quality, welfare
2. **Phenotypes and phenotyping**:
   - What is a phenotype?
   - Measurement accuracy and precision
   - Challenges in phenotyping (cost, time, invasiveness)
3. **Recording and data entry**:
   - Animal identification systems
   - Data validation and quality control
   - Database structures (brief introduction)
4. **Breeding objectives**:
   - What should we select for?
   - Single vs. multiple traits
   - Economic weights (introduce concept, detail in Chapter 9)
5. **True Breeding Value (TBV)**:
   - Definition: sum of additive effects
   - Unknown but estimable
   - Goal: rank animals by TBV

**Learning objectives**:
- Define phenotype vs. genotype
- Explain why accurate phenotyping matters
- Describe challenges in recording livestock data
- Articulate how breeding objectives guide selection
- Understand the concept of true breeding value

**Examples**:
- Growth rate in swine (electronic feeders, group vs. individual)
- Egg production in layers (trap nests, manual recording)
- Milk yield in dairy (DHI testing, milking robots)
- Feed efficiency in beef (GrowSafe, ultrasound)

**R demonstrations**:
- Reading and summarizing phenotypic data
- Data visualization (histograms, scatterplots)
- Identifying outliers and data errors
- Calculating summary statistics by contemporary group

**Interactive elements**:
- Data entry simulator (show consequences of errors)

**Key messages**:
- High-quality phenotypes are the foundation of genetic improvement
- Breeding objectives should be economically driven
- True breeding values are genetic merit we try to estimate

---

### Chapter 3: Basic Genetic Model (y = A + E)

**Purpose**: Introduce partitioning of phenotype into genetic and environmental components

**Key topics**:
1. **The basic model**: y = μ + A + E
   - y = phenotype
   - μ = population mean
   - A = additive genetic effect (breeding value)
   - E = environmental deviation
2. **Additive vs. non-additive effects**:
   - Additive genetic effects (breed true, passed to offspring)
   - Dominance effects (within-locus interaction, don't breed true)
   - Epistatic effects (between-locus interaction, complex)
3. **Why focus on additive effects?**:
   - Predictable response to selection
   - Passed from parent to offspring
   - Foundation for breeding value estimation
4. **Variance partitioning**:
   - σ²_P = σ²_A + σ²_D + σ²_E (simplified)
   - Introduce concept, full development in Chapter 5

**Learning objectives**:
- Partition phenotype into genetic and environmental components
- Distinguish additive, dominance, and epistatic effects
- Explain why additive effects drive selection response
- Understand variance decomposition conceptually

**Examples**:
- Weaning weight in swine (genetic and litter effects)
- Egg weight in layers (genetic and hen age effects)
- Milk yield in dairy (genetic and management effects)
- Birth weight in beef (genetic and dam nutrition effects)

**R demonstrations**:
- Simulate phenotypes from known genetic and environmental variances
- Visualize genetic vs. environmental contributions
- Show parent-offspring regression (introducing heritability concept)

**Interactive elements**:
- Variance decomposition simulator (adjust σ²_A and σ²_E, see effect on phenotypes)

**Key messages**:
- Phenotype is genetic + environment
- Only additive effects are reliably transmitted to offspring
- Understanding variance components is key to predicting selection response

---

### Chapter 4: Quantitative vs. Simply Inherited Traits

**Purpose**: Contrast polygenic traits with major gene effects

**Key topics**:
1. **Simply inherited traits**:
   - Mendelian inheritance (single gene, major effect)
   - Qualitative phenotypes (categories, not continuous)
   - Examples in livestock
2. **Quantitative traits**:
   - Polygenic inheritance (many genes, small effects each)
   - Continuous phenotypic distribution
   - Most economically important traits
3. **Why the distinction matters**:
   - Different breeding strategies
   - Simply inherited: can eliminate or fix alleles
   - Quantitative: gradual improvement through selection
4. **Mixed model traits**:
   - Mostly quantitative with major gene (e.g., halothane in swine)
   - Modern approach: genomic markers capture some major effects

**Learning objectives**:
- Distinguish simply inherited from quantitative traits
- Provide examples of each type in livestock
- Explain why most economic traits are quantitative
- Describe how breeding approaches differ

**Examples**:
**Simply inherited**:
- Coat color in cattle, horses (MC1R, etc.)
- Polled/horned in cattle (POLLED gene)
- Halothane sensitivity in swine (RYR1)
- Hypotrichosis (hairlessness) in cattle
- Muscular hypertrophy (myostatin) in cattle, sheep
- Genetic defects (lethal recessives)

**Quantitative**:
- Growth rate, feed efficiency
- Milk production, milk components
- Litter size, fertility
- Disease resistance
- Carcass quality traits

**R demonstrations**:
- Simulate Mendelian segregation (single gene)
- Simulate polygenic trait distribution
- Plot phenotype distributions (bimodal vs. normal)
- Calculate allele frequencies for simply inherited traits

**Interactive elements**:
- Mendelian cross simulator (show segregation ratios)

**Key messages**:
- Most important traits are quantitative (many genes)
- Simply inherited traits can be managed through genotyping
- Modern genomics bridges the gap (finding QTL in quantitative traits)

---

### Chapter 5: Heritability and Repeatability

**Purpose**: Define and interpret heritability and repeatability, core parameters for predicting selection response

**Key topics**:
1. **Heritability (h²)**:
   - Definition: h² = σ²_A / σ²_P
   - Narrow-sense vs. broad-sense (focus on narrow-sense)
   - Interpretation: proportion of phenotypic variation due to additive genetics
   - Range: 0 to 1
2. **What heritability tells us**:
   - Resemblance between relatives
   - Expected response to selection
   - Does NOT tell us:
     - Genetic vs. environmental determination (common misconception)
     - Whether a trait can be changed
     - Importance of genetics vs. environment
3. **Heritability estimation**:
   - Parent-offspring regression
   - Half-sib correlation
   - Full-sib correlation (includes non-additive effects)
   - REML from mixed models (mention, don't detail)
4. **Repeatability (r)**:
   - Definition: r = (σ²_A + σ²_PE) / σ²_P
   - σ²_PE = permanent environmental variance (affects all records on an animal)
   - Upper bound on heritability
   - Useful for repeated records (milk production, litter size)
5. **Permanent environmental effects (PE)**:
   - Effects that persist across records (udder damage, pelvic size)
   - Non-genetic but permanent
   - Important for female reproductive traits

**Learning objectives**:
- Define and calculate heritability
- Interpret heritability values for livestock traits
- Avoid common misconceptions about heritability
- Distinguish heritability from repeatability
- Explain permanent environmental effects

**Examples**:
**High heritability** (h² > 0.40):
- Body weight, growth rate
- Carcass traits (backfat, loin depth, marbling)
- Egg weight, egg production

**Moderate heritability** (h² = 0.20-0.40):
- Milk production, milk components
- Feed efficiency (RFI)
- Weaning weight (beef, swine)

**Low heritability** (h² < 0.20):
- Reproductive traits (litter size, fertility, calving ease)
- Disease resistance
- Longevity, stayability
- Temperament

**Repeatability examples**:
- Litter size in swine (r ≈ 0.15-0.20, h² ≈ 0.10-0.15)
- Milk yield in dairy (r ≈ 0.50-0.60, h² ≈ 0.30-0.40)

**R demonstrations**:
- Calculate heritability from variance components
- Parent-offspring regression
- Simulate permanent environmental effects
- Plot genetic vs. permanent environmental contributions across repeated records

**Interactive elements**:
- Heritability calculator (input variances, compute h²)
- Parent-offspring regression visualizer

**Key messages**:
- Heritability quantifies additive genetic variation
- Higher h² → faster response to selection
- Repeatability sets upper limit on heritability
- Permanent environmental effects matter for repeated traits

---

## PART 2: SELECTION AND BREEDING STRATEGIES

### Chapter 6: Breeder's Equation and Selection Response

**Purpose**: Present the breeder's equation and demonstrate how the four factors trade off

**Key topics**:
1. **Breeder's Equation**: R = i × r × σ_A × (1/L)
   - R = response to selection per year
   - i = selection intensity (standardized selection differential)
   - r = accuracy of selection (correlation between EBV and TBV)
   - σ_A = additive genetic standard deviation
   - L = generation interval
2. **Selection intensity (i)**:
   - Function of proportion selected (p)
   - Higher intensity = fewer parents selected
   - Limited by need for genetic diversity, number of offspring
   - Tables and formulas for i given p
3. **Accuracy (r)**:
   - Based on amount of information (own records, progeny, genomics)
   - Range: 0 to 1
   - Higher accuracy = more information, better ranking
   - Can be increased with progeny testing, genomic selection
4. **Genetic standard deviation (σ_A)**:
   - Measure of additive genetic variation in the population
   - σ_A = √(σ²_A) = √(h² × σ²_P)
   - Cannot easily change (but selection gradually reduces σ_A)
5. **Generation interval (L)**:
   - Average age of parents when offspring are born
   - Shorter L = faster genetic progress
   - Trade-off: shorter L may reduce accuracy (less information)
   - Varies dramatically by species (poultry: 1 year; cattle: 4-6 years)
6. **Trade-offs among the four factors**:
   - Intensity vs. generation interval (high intensity takes time)
   - Accuracy vs. generation interval (progeny testing delays selection)
   - Genomic selection resolves accuracy vs. L trade-off
7. **Comparing selection strategies**:
   - Mass selection (own performance)
   - Progeny testing (offspring performance)
   - Genomic selection (DNA-based prediction)

**Learning objectives**:
- State and apply the breeder's equation
- Explain how each factor influences response to selection
- Describe trade-offs between accuracy, intensity, and generation interval
- Compare selection strategies using the breeder's equation
- Calculate expected response to selection

**Examples**:
- **Poultry body weight**: high i, short L, moderate r → fast response
- **Dairy milk yield**: moderate i, moderate r, long L → moderate response
- **Beef weaning weight**: lower i (fewer bulls), long L, moderate r → slower response
- **Swine litter size**: low h² (low σ_A), high i, short L, low r → challenging trait

**R demonstrations**:
- Calculate selection intensity from proportion selected
- Compute expected response to selection
- Simulate multi-generation selection
- Plot genetic trends over time
- Compare strategies (mass vs. progeny test vs. genomic)

**Interactive elements**:
- **Breeder's equation calculator**: Adjust i, r, σ_A, L and see effect on R
- **Trade-off simulator**: Show impact of increasing accuracy but delaying selection

**Key messages**:
- Four factors determine rate of genetic gain
- Trade-offs exist between factors (especially r and L)
- Species differences in L create vastly different selection strategies
- Genomic selection increases r without increasing L (major advance)

---

### Chapter 7: Estimating Breeding Values

**Purpose**: Explain how we estimate breeding values, culminating in introduction to BLUP

**Key topics**:
1. **The challenge**: TBV is unknown, but we can estimate (EBV)
2. **Simple methods**:
   - Own performance (phenotype as EBV)
   - Pedigree index (midparent breeding value)
   - Progeny average (offspring mean)
   - Accuracy of each method
3. **Why simple methods fall short**:
   - Don't account for contemporary group differences (environment)
   - Don't properly weight information (varying accuracies)
   - Don't use all relatives simultaneously
4. **Contemporary groups**:
   - Animals with similar environmental conditions
   - Herd-year-season, pen, flock
   - Adjusting data for fixed effects before comparing animals
5. **Best Linear Unbiased Prediction (BLUP)**:
   - **Best**: Minimizes prediction error variance
   - **Linear**: Linear combination of data
   - **Unbiased**: Expected value equals true breeding value
   - **Prediction**: For random effects (breeding values)
6. **BLUP concepts (high-level, no MME)**:
   - Uses all information: own, ancestors, progeny, collateral relatives
   - Accounts for fixed effects (contemporary groups)
   - Weights information by accuracy
   - Shrinks toward population mean when information is sparse
7. **Understanding EBVs**:
   - Expressed as deviation from base population
   - Higher EBV = genetically superior
   - Use difference between animals, not absolute values
   - EBVs change as new data arrive (re-ranking can occur)
8. **Accuracy of EBVs**:
   - Reliability (r²): proportion of true breeding value captured
   - Increases with: more own records, progeny records, genomic data
   - Used to weight EBVs in selection decisions

**Learning objectives**:
- Estimate breeding values using simple methods
- Explain why contemporary groups must be accounted for
- Describe the purpose and advantages of BLUP
- Interpret EBVs and their accuracies
- Understand why EBVs can change over time

**Examples**:
- **Dairy**: EBVs for milk, fat, protein (Net Merit index)
- **Beef**: EPDs (Expected Progeny Differences) for weaning weight, carcass traits
- **Swine**: EBVs for growth rate, backfat, litter size
- **Poultry**: EBVs for body weight, feed efficiency, egg production

**R demonstrations**:
- Calculate EBV from own performance
- Adjust phenotypes for contemporary group effects
- Calculate progeny-based EBV
- Show how accuracy increases with more data
- Plot EBVs with confidence intervals (reflecting accuracy)

**Interactive elements**:
- **EBV calculator**: Input records for an animal and relatives, compute EBV
- **Information value visualizer**: Show how accuracy increases with data

**Key messages**:
- Estimating breeding values is the core of animal breeding
- Simple methods are intuitive but limited
- BLUP uses all information optimally
- EBVs and their accuracies guide selection decisions

---

### Chapter 8: Genetic Correlations and Correlated Response

**Purpose**: Introduce genetic correlations and their impact on multi-trait selection

**Key topics**:
1. **Genetic correlation (r_A)**:
   - Definition: correlation between additive genetic effects for two traits
   - Range: -1 to +1
   - Caused by: pleiotropy (same genes affect both traits) or linkage
2. **Interpreting genetic correlations**:
   - **Positive r_A**: selecting for trait 1 increases trait 2
   - **Negative r_A**: selecting for trait 1 decreases trait 2 (antagonistic)
   - **Zero r_A**: traits are genetically independent
3. **Correlated response to selection**:
   - CR_Y = i × r_X × r_A(X,Y) × σ_A(Y) × (1/L)
   - Selecting on trait X causes response in trait Y
   - Magnitude depends on r_A and genetic variation in both traits
4. **Why genetic correlations matter**:
   - Can't improve all traits simultaneously if r_A is negative
   - Must balance selection for multiple traits (multi-trait selection)
   - Some correlations are favorable (growth rate and feed intake)
   - Some correlations are unfavorable (milk yield and fertility in dairy)
5. **Examples of genetic correlations**:
   - **Positive**: backfat and growth rate (undesirable in swine)
   - **Negative**: milk yield and reproductive performance (dairy)
   - **Negative**: growth rate and leg soundness (broilers)
   - **Positive**: carcass traits (loin depth and % lean)

**Learning objectives**:
- Define genetic correlation
- Interpret positive, negative, and zero genetic correlations
- Calculate correlated response to selection
- Explain why antagonistic correlations complicate breeding programs
- Provide examples of important genetic correlations in livestock

**Examples**:
- **Dairy cattle**: Milk yield vs. fertility (r_A ≈ -0.3 to -0.4)
- **Broilers**: Growth rate vs. leg problems (r_A ≈ 0.3-0.5, unfavorable)
- **Layers**: Egg production vs. egg weight (r_A ≈ -0.2 to -0.4)
- **Swine**: Backfat vs. average daily gain (r_A ≈ 0.3-0.4)
- **Beef**: Marbling vs. lean growth (r_A near zero or slightly negative)

**R demonstrations**:
- Calculate correlated response to selection
- Simulate selection on trait X and observe change in trait Y
- Plot bivariate distributions showing genetic correlation
- Show trade-offs when r_A is negative

**Interactive elements**:
- **Genetic correlation simulator**: Adjust r_A, select on trait X, visualize correlated response in trait Y

**Key messages**:
- Traits are genetically correlated due to pleiotropy or linkage
- Negative genetic correlations create breeding challenges
- Correlated response can be favorable or unfavorable
- Multi-trait selection is necessary to balance improvement

---

### Chapter 9: Multiple Trait Selection and Selection Index

**Purpose**: Present methods for simultaneous improvement of multiple traits

**Key topics**:
1. **The need for multi-trait selection**:
   - Most breeding goals involve multiple traits
   - Economic values differ across traits
   - Genetic correlations may be antagonistic
2. **Breeding goal (H)** vs. **Selection index (I)**:
   - **Breeding goal**: Traits we want to improve, weighted by economic values
   - **Selection index**: Information we use to rank animals (may include correlated traits)
   - Not always the same traits in H and I
3. **Selection index theory**:
   - I = b₁X₁ + b₂X₂ + ... + bₙXₙ
   - b = vector of index weights
   - X = vector of phenotypes or EBVs
   - Weights (b) chosen to maximize correlation between I and H
4. **Calculating index weights**:
   - Requires: genetic parameters (h², r_A), economic weights (v)
   - Index equation: b = P⁻¹ G v
   - P = phenotypic (co)variance matrix
   - G = genetic (co)variance matrix
   - v = vector of economic weights
5. **Economic weights**:
   - Profit per unit change in trait (holding others constant)
   - Typically $/unit (e.g., $/kg milk, $/day to market)
   - Derived from profit functions or market prices
6. **Interpreting index weights**:
   - Larger |b| = more weight on that trait in selection decisions
   - Sign of b can differ from sign of economic weight (due to correlations)
7. **Examples of selection indices**:
   - **Dairy**: Net Merit Index (milk, fat, protein, fertility, health, longevity)
   - **Beef**: Terminal Index (growth, carcass quality) vs. Maternal Index (reproduction, maternal ability)
   - **Swine**: Sow productivity index (litter size, piglet survival) vs. Growth index (ADG, FCR, backfat)
   - **Layers**: Egg production, egg weight, feed efficiency, shell quality

**Learning objectives**:
- Distinguish breeding goal from selection index
- Explain why economic weights are necessary
- Describe how genetic correlations influence index weights
- Calculate a simple selection index
- Interpret index values and selection decisions

**Examples**:
- **Dairy Net Merit**: Economic values for yield, health, fertility
- **Swine sow index**: Economic values for litter size, piglet survival, longevity
- **Beef terminal index**: Economic values for growth rate, feed efficiency, carcass value

**R demonstrations**:
- Calculate economic weights from profit function
- Compute selection index weights (b = P⁻¹ G v)
- Rank animals by index value
- Compare selection decisions with vs. without index
- Simulate response to index selection

**Interactive elements**:
- **Index weight calculator**: Input economic weights and genetic parameters, compute index weights
- **Index selection simulator**: Adjust economic weights, see how selection decisions change

**Key messages**:
- Multiple traits require multi-trait selection
- Selection index optimally combines information
- Economic weights drive the breeding goal
- Index weights account for genetic correlations and heritabilities

---

## PART 3: INBREEDING, MATING, AND CROSSBREEDING

### Chapter 10: Mating Strategies and Optimum Contribution Selection

**Purpose**: Explain mating decisions, crossbreeding strategies, and modern mating optimization

**Key topics**:
1. **Mating vs. selection**:
   - **Selection**: Which animals become parents?
   - **Mating**: Which parents are mated to each other?
   - Both decisions affect genetic gain and genetic diversity
2. **Types of mating systems**:
   - **Random mating**: Mates chosen at random
   - **Assortative mating**: Positive (like to like) or negative (unlike to like)
   - **Inbreeding**: Mating of related individuals (usually avoided)
   - **Crossbreeding**: Mating animals from different breeds (discussed in Chapter 11)
3. **Mating to manage inbreeding**:
   - Inbreeding depression (reduced performance in inbred offspring)
   - Minimum coancestry mating (pair animals to minimize relationship)
   - Balance: genetic gain vs. inbreeding
4. **Compensatory mating**:
   - Mate animals with complementary strengths/weaknesses
   - Reduce variation in offspring quality
   - Common in terminal sire systems
5. **Optimum Contribution Selection (OCS)**:
   - Simultaneously optimize selection and mating decisions
   - Maximize genetic gain subject to inbreeding constraint
   - Modern approach implemented in software (MateSel, AlphaMate, etc.)
   - Determines: how many offspring per parent, which matings to make
6. **Software for mating decisions**:
   - **MateSel**: Optimizes mate allocations to maximize index value while constraining inbreeding
   - **AlphaMate**: Research tool for OCS
   - Used by commercial breeding companies
7. **Rotational crossbreeding** (introduction, detailed in Chapter 11):
   - Two-breed rotation, three-breed rotation
   - Maintains heterosis over time

**Learning objectives**:
- Distinguish selection from mating decisions
- Explain why mating strategies matter (inbreeding, genetic diversity)
- Describe optimum contribution selection and its purpose
- Identify software tools used for mating optimization
- Understand basic rotational crossbreeding schemes

**Examples**:
- **Dairy**: Genomic selection allows more intense selection, but increases inbreeding risk → need mating optimization
- **Swine**: Three-breed rotational cross (maternal breeds)
- **Beef**: Terminal sire on crossbred cows (compensatory mating)
- **Poultry**: Within-line mating optimization to manage inbreeding in closed nucleus populations

**R demonstrations**:
- Calculate inbreeding coefficient from pedigree
- Simulate random vs. minimum coancestry mating
- Show impact of OCS on genetic gain and inbreeding
- Demonstrate rotational crossbreeding (allele frequencies over generations)

**Interactive elements**:
- **Mating simulator**: Select animals, choose mating strategy, observe inbreeding and genetic gain
- **Rotational cross visualizer**: Animate breed composition over generations

**Key messages**:
- Mating decisions affect inbreeding and genetic diversity
- Optimum contribution selection balances gain and inbreeding
- Software tools implement complex mating optimization
- Rotational crossbreeding maintains hybrid vigor

---

### Chapter 11: Crossbreeding and Hybrid Vigor

**Purpose**: Explain crossbreeding systems, heterosis, and industry breeding structures

**Key topics**:
1. **What is crossbreeding?**:
   - Mating animals from different breeds or lines
   - Produces crossbred (hybrid) offspring
   - Widely used in swine, beef, poultry, sheep
   - Less common in dairy, horses
2. **Hybrid vigor (heterosis)**:
   - Increased performance of crossbred offspring compared to purebred parents
   - H = Performance_crossbred - Average_performance_purebreds
   - Often expressed as percentage of purebred average
3. **What controls heterosis?**:
   - **Dominance**: Crossbreds mask recessive deleterious alleles
   - **Overdominance**: Heterozygotes superior to both homozygotes (rare)
   - **Epistasis**: Favorable interactions between alleles from different breeds
   - Magnitude depends on genetic distance between breeds
4. **Traits with significant heterosis**:
   - **High heterosis**: Reproductive traits (litter size, fertility, survival) – 5-20%
   - **Moderate heterosis**: Growth traits, feed efficiency – 2-10%
   - **Low heterosis**: Carcass traits, milk production – 0-5%
5. **Crossbreeding systems**:
   - **Terminal cross**: Purebred or F₁ females × terminal sire (all offspring sold)
   - **Two-breed rotation**: Alternate breeds each generation (maintains 67% heterosis)
   - **Three-breed rotation**: Three breeds in rotation (maintains 86% heterosis)
   - **Composite breeds**: Stabilized crossbreds (fixed breed composition)
   - **Rotational terminal cross**: Rotation for females, terminal sire for market offspring
6. **Industry structure by species**:
   - **Swine**: F₁ females (Large White × Landrace) × terminal sire (Duroc, Pietrain, synthetic lines)
   - **Beef**: Crossbred cows (various breeds) × terminal sire (Angus, Charolais, etc.)
   - **Poultry**: Proprietary synthetic lines crossed to produce commercial birds (not breed-based)
   - **Sheep**: Terminal sire breeds (Suffolk, Hampshire) on crossbred ewes
   - **Dairy**: Mostly purebred Holsteins; some use of crossbreeding (Holstein × Jersey × other)
7. **Genetic evaluation in crossbreeding**:
   - Pure breed vs. crossbred performance
   - GCA (General Combining Ability) and SCA (Specific Combining Ability)
   - Modern genomic evaluations can estimate crossbred performance

**Learning objectives**:
- Define heterosis and explain its genetic basis
- Describe which traits show high vs. low heterosis
- Compare crossbreeding systems (terminal, rotational, composite)
- Explain industry breeding structures in swine, beef, and poultry
- Calculate expected heterosis in different crossbreeding schemes

**Examples**:
- **Swine litter size**: 1-2 more pigs born alive in crossbreds (10-15% heterosis)
- **Beef calf survival**: 5-10% improvement in crossbreds
- **Dairy milk yield**: Minimal heterosis (0-5%)
- **Broiler growth rate**: Moderate heterosis in commercial crosses (3-7%)

**R demonstrations**:
- Calculate heterosis from purebred and crossbred performance data
- Simulate rotational crossbreeding (breed composition over generations)
- Simulate expected heterosis in two-breed and three-breed rotations
- Compare genetic progress in purebred vs. crossbred systems

**Interactive elements**:
- **Crossbreeding system simulator**: Choose breeds, system (terminal, rotation), visualize breed composition and heterosis over generations

**Key messages**:
- Crossbreeding exploits heterosis, especially for fitness traits
- Different crossbreeding systems maintain different levels of heterosis
- Industry structures optimize heterosis and selection response
- Swine and poultry use highly structured crossbreeding programs

---

## PART 4: GENOMICS

### Chapter 12: Introduction to Genomics

**Purpose**: Introduce genomic technologies and their role in animal breeding

**Key topics**:
1. **What is genomics in breeding?**:
   - Using DNA information to improve genetic predictions
   - Complements traditional pedigree and phenotypic information
   - Revolutionized animal breeding since ~2008
2. **DNA markers: SNPs (Single Nucleotide Polymorphisms)**:
   - Most common genetic variant (one nucleotide difference)
   - Millions of SNPs across the genome
   - Can be genotyped with SNP chips (arrays)
3. **SNP panels (chips)**:
   - Arrays with 10K, 50K, 600K, or more SNPs
   - Cost has decreased dramatically (now $30-$150 per animal)
   - Species-specific panels (Bovine SNP50, Porcine SNP60, etc.)
4. **Bioinformatics basics**:
   - Processing sequencing data (brief overview, not detailed)
   - Quality control (call rate, minor allele frequency, Hardy-Weinberg)
   - Imputation (predicting missing genotypes from low- to high-density)
5. **Whole genome sequencing (WGS)**:
   - Sequencing entire genome (~3 billion bp in mammals)
   - Captures all genetic variation (SNPs, indels, structural variants)
   - Still expensive per animal ($500-$2000), but falling
   - Used for finding causal variants, imputation reference
6. **From genotypes to genomic predictions**:
   - Genotypes used to predict breeding values (GEBV = Genomic EBV)
   - Discussed in detail in Chapter 13
7. **Applications of genomics**:
   - Genomic selection (increased accuracy and reduced generation interval)
   - Parentage verification and pedigree correction
   - Identification of causal mutations (GWAS)
   - Genomic management of inbreeding

**Learning objectives**:
- Explain what a SNP is and why SNPs are useful markers
- Describe SNP chips and their use in livestock breeding
- Understand the basics of genotype quality control
- Distinguish SNP chips from whole genome sequencing
- Identify applications of genomics in animal breeding

**Examples**:
- **Dairy**: BovineHD SNP chip (777K SNPs), used for genomic selection since 2009
- **Swine**: PorcineSNP60 chip, used for genomic selection in breeding companies
- **Poultry**: Custom Axiom SNP arrays (600K SNPs), proprietary by companies
- **Beef**: GGP-F250 chip (250K SNPs), used for genomic EPDs

**R demonstrations**:
- Load and explore SNP genotype data (0, 1, 2 format)
- Calculate allele frequencies
- Perform basic quality control (missing data, MAF)
- Visualize genotype distributions
- Calculate genomic relationship matrix (preview for Chapter 13)

**Interactive elements**:
- **Genotype explorer**: Visualize SNP data for a few animals
- **Relationship calculator**: Compare pedigree vs. genomic relationships

**Key messages**:
- Genomics uses DNA markers (SNPs) to improve predictions
- SNP chips are cost-effective and widely used
- Genomic information increases accuracy of breeding values
- Whole genome sequencing provides ultimate resolution

---

### Chapter 13: Genomic Selection

**Purpose**: Explain how genomic information is used to predict breeding values

**Key topics**:
1. **What is genomic selection?**:
   - Predicting breeding values using genome-wide SNP data
   - Eliminates need for own phenotypes or progeny testing
   - Enables selection at birth (or even embryo stage)
2. **Why genomic selection works**:
   - SNPs in linkage disequilibrium (LD) with causal mutations
   - Thousands of SNPs across genome capture additive genetic variation
   - Training population: animals with genotypes and phenotypes
   - Genomic predictions applied to selection candidates
3. **Two main modeling approaches**:
   - **Animal model**: Predict breeding values directly (GBLUP)
   - **Marker effects model**: Estimate effect of each SNP, sum to get GEBV (SNP-BLUP, Bayesian methods)
4. **GBLUP (Genomic BLUP)**:
   - Extension of traditional BLUP using genomic relationship matrix (G)
   - G matrix computed from SNP genotypes
   - Captures realized relationships (Mendelian sampling)
   - More accurate than pedigree-based BLUP
5. **SNP-BLUP and marker effects models**:
   - Estimate effect of each SNP (thousands of effects)
   - SNP-BLUP: assumes all SNPs have equal variance
   - Equivalent to GBLUP under certain assumptions
6. **Bayesian methods**:
   - BayesA, BayesB, BayesC, BayesCπ, Bayesian Lasso
   - Allow SNPs to have different variance (some large effects, many small)
   - Can improve accuracy for traits with major QTL
   - Computationally intensive
7. **Single-step genomic BLUP (ssGBLUP)**:
   - Developed by Ignacy Misztal, Rohan Fernando, and others
   - Combines pedigree and genomic information in one analysis
   - Uses H matrix (blends A and G matrices)
   - Allows genotyped and non-genotyped animals in same evaluation
   - Widely used in dairy, beef, swine, and poultry
8. **Accuracy of genomic predictions**:
   - Depends on: size of training population, heritability, effective population size, LD
   - Typically 0.40-0.70 for young animals without own phenotypes
   - Much higher than parent average (0.30-0.40)
9. **Impact of genomic selection**:
   - Doubled rate of genetic gain in dairy cattle
   - Reduced generation interval (no need for progeny testing)
   - Increased selection intensity (can genotype many candidates)
   - Reduced costs (genomic testing cheaper than progeny testing)

**Learning objectives**:
- Explain the principles of genomic selection
- Distinguish GBLUP, SNP-BLUP, and Bayesian methods
- Understand single-step genomic BLUP and its advantages
- Describe the impact of genomic selection on livestock breeding
- Recognize the importance of training population size

**Examples**:
- **Dairy cattle**: Genomic selection for young bulls (eliminated progeny testing for most traits)
- **Swine**: Genomic selection for feed efficiency (expensive to measure phenotypically)
- **Poultry**: Genomic selection for disease resistance, egg production
- **Beef**: Genomic EPDs using single-step GBLUP

**R demonstrations**:
- Calculate genomic relationship matrix (G) from SNP genotypes
- Simulate genomic prediction (training + validation)
- Calculate accuracy of genomic predictions
- Compare GBLUP vs. traditional BLUP accuracies
- Show impact of training population size on accuracy

**Interactive elements**:
- **Genomic prediction accuracy simulator**: Adjust training population size, heritability, see effect on accuracy
- **Single-step vs. multi-step comparison**: Visualize differences

**Key messages**:
- Genomic selection uses genome-wide SNP data to predict breeding values
- GEBVs are much more accurate than parent average
- Single-step GBLUP is the standard approach in industry
- Genomic selection has revolutionized animal breeding (faster genetic progress)

---

## PART 5: PRACTICAL SKILLS

### Chapter 14: Practical Animal Breeding and Data Skills

**Purpose**: Equip students with practical skills for working in animal breeding

**Key topics**:
1. **Database basics**:
   - Relational database concepts (tables, keys, relationships)
   - **SQL (Structured Query Language)** – very basics only:
     - SELECT, WHERE, JOIN (simple examples)
     - Purpose: extract phenotypic data for genetic evaluation
     - Not an SQL course, just awareness
2. **APIs (Application Programming Interfaces)**:
   - What is an API? (interface to query databases or services)
   - Example: Query genomic database for genotypes
   - Example: Query USDA breed association data
   - Using R to access APIs (httr package)
3. **Data management**:
   - Data entry and validation
   - Cleaning and quality control
   - Data transformation and preparation for genetic evaluation
   - Version control and documentation (brief mention)
4. **Animal identification systems**:
   - Electronic ID (RFID ear tags)
   - Visual ID (ear tags, tattoos, brands)
   - DNA-based parentage verification
   - Record linkage across databases
5. **Phenotypic culling vs. genetic selection**:
   - **Phenotypic culling**: Remove animals that fail to meet minimum standards (health, reproductive failure)
   - **Genetic selection**: Choose parents based on EBVs
   - Both are important; different goals
6. **Working with breeding companies**:
   - Roles: geneticist, data manager, reproductive technician, field staff
   - Data flow: field → database → genetic evaluation → selection decisions
   - Software used in industry: BLUPF90, ASReml, specialized company tools
7. **Professional skills**:
   - Communication (explaining genetics to producers)
   - Collaboration (working with multidisciplinary teams)
   - Ethics (data integrity, animal welfare)

**Learning objectives**:
- Understand basics of SQL for querying breeding databases
- Explain what APIs are and how they are used
- Describe animal identification systems
- Distinguish phenotypic culling from genetic selection
- Identify career opportunities in animal breeding

**Examples**:
- **SQL query**: Extract phenotypic data for animals born in 2023
- **API example**: Use CDCB (Council on Dairy Cattle Breeding) API to get genomic evaluations
- **Animal ID**: RFID tags in swine, visual tags in beef cattle
- **Data cleaning**: Identify and correct errors in birth weights

**R demonstrations**:
- SQL queries using DBI and RSQLite packages (simple SELECT, JOIN)
- Access an API using httr or httr2 package
- Data validation and cleaning (outliers, missing data, duplicates)
- Merge phenotypic and pedigree data
- Generate reports for breeding decisions

**Interactive elements**:
- **SQL query builder**: Interactive tool to construct simple SELECT statements
- **API explorer**: Query a public genomic database

**Key messages**:
- Practical skills are essential for applying breeding theory
- Data management is foundational to genetic evaluation
- Animal breeding involves teamwork and communication
- Many career paths exist in animal breeding

---

## PART 6: SPECIES-SPECIFIC BREEDING

### Chapter 15: Swine Breeding

**Purpose**: Comprehensive overview of commercial swine breeding programs, traits, and industry structure

**Key topics**:
1. **Global swine industry structure**:
   - Major breeding companies (Genus/PIC, Topigs Norsvin, Genesus, Smithfield, etc.)
   - Three-tier breeding pyramid (nucleus, multiplier, commercial)
   - Pure lines vs. crossbreds
   - Global genetics flow and regional adaptation
2. **Key traits and heritabilities**:
   - **Maternal traits**: Litter size (TNB, NBA, NW), piglet survival, weaning weight, maternal ability (low h²: 0.10-0.15)
   - **Growth traits**: ADG, backfat depth, loin depth, feed efficiency/RFI (moderate to high h²: 0.30-0.50)
   - **Meat quality**: pH, color, marbling, drip loss (moderate h²: 0.20-0.40)
   - **Reproduction**: Age at puberty, farrowing interval, longevity (low to moderate h²)
   - **Health and welfare**: Disease resistance, leg soundness, temperament
3. **Crossbreeding systems**:
   - Terminal sire lines (Duroc, Pietrain, synthetic lines) for growth and carcass
   - Maternal lines (Large White, Landrace) for reproduction
   - F₁ females (Large White × Landrace) in commercial production
   - Rotational systems for maintaining heterosis
4. **Selection indices**:
   - Terminal sire index (growth, feed efficiency, carcass traits)
   - Maternal index (litter size, piglet survival, maternal ability, longevity)
   - Economic weights and derivation
5. **Genomic selection in swine**:
   - Implementation timeline (widespread since ~2012)
   - Genomic tools (PorcineSNP60, GeneSeek GGP-Porcine)
   - Impact on accuracy and generation interval
   - Selection for hard-to-measure traits (RFI, meat quality)
6. **Reproductive technologies**:
   - AI and semen distribution
   - Estrus synchronization
   - Emerging: sexed semen, embryo transfer, gene editing (PRRS resistance)
7. **Challenges and opportunities**:
   - Balancing growth with reproduction
   - Disease challenges (PRRS, PED, ASF)
   - Welfare (tail biting, aggression, farrowing crate alternatives)
   - Feed efficiency and sustainability

**Learning objectives**:
- Describe the three-tier swine breeding structure
- Explain the distinction between terminal and maternal breeding objectives
- Identify key traits and their genetic parameters in swine
- Design a crossbreeding program for commercial swine production
- Understand the role of genomic selection in modern swine breeding

**Examples**:
- PIC breeding pyramid and product portfolio (PIC308, PIC310, PIC337, PIC800)
- Maternal line selection emphasizing litter size and piglet survival
- Terminal sire selection emphasizing growth rate, feed efficiency, and carcass merit
- Case study: Improving RFI with genomic selection

**R demonstrations**:
- Simulate swine crossbreeding system (breed composition, heterosis)
- Calculate economic weights for maternal vs. terminal indices
- Compare selection response for litter size (low h²) vs. backfat (high h²)
- Estimate genetic trends in commercial swine populations

**Interactive elements**:
- Swine crossbreeding system simulator (visualize F₁, terminal cross, rotational options)
- Maternal vs. terminal index weight calculator

**Key messages**:
- Swine breeding is highly structured with distinct maternal and terminal lines
- Crossbreeding exploits heterosis for reproductive traits
- Genomic selection has accelerated genetic progress, especially for expensive traits
- Economic weights differ dramatically between maternal and terminal objectives

---

### Chapter 16: Poultry Breeding

**Purpose**: Explain unique features of poultry breeding with separate sections for broilers, layers, and turkeys

**Key topics**:
1. **Global poultry industry structure**:
   - Vertical integration (genetics, hatchery, grow-out, processing)
   - Major breeding companies (Cobb-Vantress, Aviagen, Hy-Line International, Hendrix Genetics)
   - Proprietary synthetic lines (not traditional breed-based)
   - Closed nucleus populations
2. **Unique features of poultry breeding**:
   - Short generation intervals (9-12 months)
   - High selection intensity (thousands of candidates evaluated)
   - Family-based selection (sib testing, pedigree hatching)
   - Rapid genetic progress possible
   - Strict biosecurity requirements

**Section A: Broiler Breeding**

**Key topics**:
1. **Broiler traits and heritabilities**:
   - **Growth traits**: Body weight at processing age (high h²: 0.30-0.50)
   - **Feed efficiency**: FCR, RFI (moderate h²: 0.25-0.40)
   - **Carcass traits**: Breast yield, leg yield, abdominal fat (moderate to high h²)
   - **Leg health**: Leg soundness, tibial dyschondroplasia, footpad lesions (low to moderate h²)
   - **Livability and welfare**: Mortality, ascites, sudden death syndrome (low h²)
   - **Reproductive fitness** (in parent stock): Egg production, fertility, hatchability (low to moderate h²)
2. **Breeding objectives**:
   - Balance rapid growth with welfare and reproductive fitness
   - Economic weights: feed cost, processing yield, mortality
   - Selection indices incorporating 10+ traits
3. **Crossbreeding**:
   - Four-way crosses common (sire line × dam line)
   - Sire line: emphasis on growth and carcass yield
   - Dam line: emphasis on reproduction, livability, and egg production
4. **Challenges**:
   - Genetic correlations between growth and leg problems
   - Balancing parent stock fitness with commercial performance
   - Welfare concerns (rapid growth, mobility issues)

**Section B: Egg-Laying Hen Breeding**

**Key topics**:
1. **Layer traits and heritabilities**:
   - **Egg production**: Total eggs, rate of lay, persistency (moderate h²: 0.20-0.40)
   - **Egg quality**: Egg weight, shell strength, shell color, internal quality (moderate to high h²)
   - **Feed efficiency**: Feed per egg, RFI (moderate h²: 0.25-0.35)
   - **Livability**: Mortality, disease resistance, keel bone damage (low h²)
   - **Behavior and welfare**: Feather pecking, fearfulness, nesting behavior (low to moderate h²)
2. **Brown vs. white egg layers**:
   - Different genetic lines and breeding objectives
   - Market preferences by region
3. **Breeding objectives**:
   - Maximize eggs per hen housed
   - Improve egg quality (shell strength, size uniformity)
   - Reduce feed cost per dozen eggs
   - Enhance welfare (reduce feather pecking, improve bone strength)
4. **Cage-free and alternative housing systems**:
   - New selection pressures (nesting, perching, floor eggs)
   - Keel bone damage as emerging trait

**Section C: Turkey Breeding**

**Key topics**:
1. **Turkey traits and heritabilities**:
   - **Growth**: Body weight at 16-20 weeks (high h²: 0.30-0.50)
   - **Carcass traits**: Breast yield, leg yield (moderate to high h²)
   - **Leg health and welfare**: Leg soundness, mobility (low to moderate h²)
   - **Reproduction**: Fertility, hatchability (very low h²: 0.05-0.15)
2. **Unique challenges**:
   - Reproductive fitness severely compromised by selection for growth
   - Nearly all breeding via artificial insemination
   - Extreme sexual dimorphism (males 2x larger than females)
3. **Breeding structure**:
   - Separate male and female lines
   - Selection emphasis differs by sex

**Learning objectives**:
- Describe the structure of integrated poultry breeding companies
- Explain why poultry breeding allows rapid genetic progress
- Compare breeding objectives for broilers, layers, and turkeys
- Identify major genetic correlations affecting poultry breeding (growth vs. leg health, egg production vs. egg weight)
- Understand the role of family-based selection in poultry

**Examples**:
- Cobb500 broiler: product profile and genetic background
- Hy-Line Brown layer: breeding objective and index
- Genetic trends in broiler growth rate (1950s to present)
- Case study: Improving leg health while maintaining growth

**R demonstrations**:
- Simulate multi-generation selection in broilers (growth vs. leg health trade-off)
- Calculate index weights for layer breeding (eggs, egg quality, feed efficiency)
- Estimate response to family selection
- Plot genetic trends in commercial broiler lines

**Interactive elements**:
- Broiler breeding objective simulator (adjust economic weights, visualize selection response)
- Layer performance calculator (eggs per hen, feed cost, revenue)

**Key messages**:
- Poultry breeding is the most intensive and rapid form of livestock breeding
- Short generation intervals and high selection intensity enable fast progress
- Genetic correlations between production and welfare require balanced selection
- Industry consolidation means a few companies supply global genetics

---

### Chapter 17: Dairy Cattle Breeding

**Purpose**: Deep dive into dairy cattle breeding, focusing on the transition to genomic selection

**Key topics**:
1. **Global dairy industry structure**:
   - Major breeds (Holstein, Jersey, Brown Swiss, others)
   - AI organizations (cooperative and private): Select Sires, ABS Global, CRV, Semex, Alta Genetics
   - Genomic testing companies and service providers
   - International semen trade
2. **Key traits and heritabilities**:
   - **Production traits**: Milk yield, fat yield, protein yield, fat %, protein % (moderate h²: 0.25-0.40)
   - **Fertility and reproduction**: Daughter pregnancy rate, calving ease, calving interval (low h²: 0.05-0.10)
   - **Health traits**: Mastitis resistance, lameness, metabolic disorders (low h²: 0.05-0.15)
   - **Longevity**: Productive life, stayability (low h²: 0.10-0.15)
   - **Conformation**: Udder, feet/legs, body size (moderate h²: 0.20-0.40)
   - **Feed efficiency**: RFI, dry matter intake (moderate h²: 0.25-0.35)
   - **Methane emissions**: Emerging trait (low to moderate h²)
3. **Genetic correlations**:
   - **Antagonistic**: Milk yield vs. fertility (r_A ≈ -0.3 to -0.4)
   - **Antagonistic**: Milk yield vs. health (r_A ≈ -0.2 to -0.3)
   - **Favorable**: Conformation traits and longevity (r_A ≈ 0.3-0.5)
4. **Selection indices**:
   - **Net Merit (NM$)**: US lifetime profit index
   - **Cheese Merit (CM$)**: Emphasizes fat and protein over volume
   - **Fluid Merit (FM$)**: Emphasizes milk volume
   - **Genomic Merit indices** (various countries)
   - Economic weights: production, fertility, health, longevity
5. **Genomic selection revolution in dairy**:
   - Timeline: Implemented ~2009 in US, rapidly adopted globally
   - Eliminated need for progeny testing for most bulls
   - Reduced generation interval from 6-7 years to 2-3 years
   - Doubled rate of genetic gain
   - Training population size and accuracy
   - Single-step GBLUP implementation (CDN, USDA, etc.)
6. **Progeny testing (historical context)**:
   - Young bull sampling programs (pre-genomic era)
   - Daughter performance evaluations
   - Why progeny testing is now limited to elite sires
7. **Crossbreeding in dairy**:
   - ProCROSS system (Holstein × Montbéliarde × Viking Red)
   - Heterosis for fertility and health
   - Trade-offs with milk production
8. **Reproductive technologies**:
   - Widespread AI (>95% in commercial dairy)
   - Sexed semen (increase heifer calves, improve genetic progress)
   - Embryo transfer and IVF
   - Gene editing (polled allele, disease resistance)

**Learning objectives**:
- Describe the structure of the dairy breeding industry
- Explain how genomic selection transformed dairy cattle breeding
- Identify key traits and genetic parameters in dairy cattle
- Interpret selection indices (Net Merit, Cheese Merit)
- Understand antagonistic genetic correlations affecting breeding objectives
- Compare pre-genomic and genomic-era breeding strategies

**Examples**:
- Case study: Elite genomic young sire (high GTPI, high reliability)
- Net Merit index composition and economic weights
- Genetic trends in US Holsteins (1960-2025)
- ProCROSS vs. Holstein comparison

**R demonstrations**:
- Calculate Net Merit index from EBVs and economic weights
- Simulate impact of genomic selection on generation interval and genetic gain
- Compare progeny testing vs. genomic selection (accuracy, cost, time)
- Visualize genetic correlations between milk yield and fertility

**Interactive elements**:
- Net Merit calculator (input trait EBVs, compute index)
- Genomic vs. progeny testing comparison tool
- Crossbreeding system simulator for dairy

**Key messages**:
- Dairy cattle breeding was revolutionized by genomic selection
- Genomic selection increased accuracy while reducing generation interval
- Balancing production with fertility and health is critical
- Economic indices guide selection decisions

---

### Chapter 18: Beef Cattle Breeding

**Purpose**: Explain beef cattle breeding with emphasis on seedstock industry, EPDs, and crossbreeding

**Key topics**:
1. **Beef industry structure**:
   - Seedstock producers (purebred breeders)
   - Commercial cow-calf operations
   - Breed associations (American Angus Association, Red Angus, Hereford, Simmental, etc.)
   - Vertical integration less common than in other species
2. **Breed diversity**:
   - **British breeds**: Angus, Hereford, Red Angus, Shorthorn (moderate size, early maturity, marbling)
   - **Continental breeds**: Charolais, Simmental, Limousin, Gelbvieh (larger size, lean growth, terminal sires)
   - **Composite breeds**: Brangus, Beefmaster, Santa Gertrudis (stabilized crosses)
   - **Brahman influence**: Heat tolerance, parasite resistance
3. **Key traits and heritabilities**:
   - **Growth traits**: Birth weight, weaning weight, yearling weight, ADG (moderate to high h²: 0.30-0.50)
   - **Carcass traits**: Marbling, ribeye area, backfat, yield grade (moderate to high h²: 0.35-0.50)
   - **Maternal traits**: Milk production (dam's maternal ability), mature cow size, calving ease (low to moderate h²: 0.10-0.30)
   - **Reproduction**: Heifer pregnancy, scrotal circumference, docility (low to moderate h²: 0.10-0.30)
   - **Feed efficiency**: RFI (moderate h²: 0.30-0.40)
4. **EPDs (Expected Progeny Differences)**:
   - Definition and interpretation
   - Accuracy values
   - Comparing EPDs across breeds (breed adjustments)
   - Using EPDs for selection decisions
5. **Selection indices**:
   - **Terminal indices**: Emphasize growth and carcass value (feedlot and carcass merit)
   - **Maternal indices**: Emphasize calving ease, maternal ability, moderate size
   - **All-purpose indices**: Balance multiple objectives
   - Economic weights by production system
6. **Crossbreeding systems**:
   - **Terminal cross**: Crossbred cows × terminal sire (all calves sold)
   - **Rotational systems**: Two-breed or three-breed rotation
   - **Composite breeds**: Fixed breed composition
   - Heterosis for maternal traits (reproduction, longevity, calf survival)
7. **Genomic selection in beef**:
   - Slower adoption than dairy (less integration, smaller reference populations)
   - Genomic-enhanced EPDs (GE-EPDs)
   - Low-density and high-density SNP panels
   - Single-step GBLUP implementation by breed associations
8. **Challenges and opportunities**:
   - Balancing growth with calving ease and maternal efficiency
   - Feed efficiency and sustainability
   - Regional adaptation (heat tolerance, fescue toxicosis)
   - Emerging traits (methane emissions, tenderness)

**Learning objectives**:
- Describe the structure of the beef cattle breeding industry
- Interpret EPDs and use them for sire selection
- Compare terminal and maternal breeding objectives
- Design a crossbreeding system for commercial beef production
- Understand the role of breed associations in genetic evaluation
- Explain the benefits of heterosis in beef cattle

**Examples**:
- Selecting a terminal sire using EPDs (Angus bull for marbling and growth)
- Comparing maternal vs. terminal sire EPD profiles
- Case study: Rotational crossbreeding system (Angus × Simmental × Gelbvieh)
- Genetic trends in Angus cattle (marbling, growth, calving ease)

**R demonstrations**:
- Calculate EPDs from phenotypic data (simple example)
- Simulate rotational crossbreeding (breed composition, heterosis over time)
- Compare terminal vs. maternal index selection
- Estimate economic returns from genetic improvement

**Interactive elements**:
- EPD calculator and sire comparison tool
- Beef crossbreeding system simulator
- Terminal vs. maternal index weight calculator

**Key messages**:
- Beef cattle breeding is decentralized with many independent breeders
- EPDs are the standard genetic evaluation tool
- Crossbreeding exploits heterosis for maternal traits
- Terminal and maternal objectives require different selection strategies

---

### Chapter 19: Sheep Breeding

**Purpose**: Overview of sheep breeding with emphasis on wool, meat, and dual-purpose breeds

**Key topics**:
1. **Global sheep industry and diversity**:
   - Major sheep-producing regions (Australia, New Zealand, China, UK, US)
   - Breed diversity: wool, meat, dual-purpose, hair sheep
   - Industry structure varies by region (large-scale grazing vs. small farm flocks)
2. **Breed types and objectives**:
   - **Wool breeds**: Merino (fine wool production)
   - **Meat breeds**: Suffolk, Hampshire, Dorset (terminal sires for market lambs)
   - **Dual-purpose breeds**: Polypay, Columbia, Targhee
   - **Maternal breeds**: Rambouillet, Polypay (prolificacy, maternal ability)
   - **Hair sheep**: Katahdin, Dorper (no shearing required, parasite resistance)
3. **Key traits and heritabilities**:
   - **Growth traits**: Birth weight, weaning weight, post-weaning gain (moderate to high h²: 0.25-0.45)
   - **Carcass traits**: Loin eye area, fat depth, leg score (moderate h²: 0.25-0.40)
   - **Reproduction**: Litter size (lambs born), fertility, lambing interval (low h²: 0.10-0.15)
   - **Wool traits**: Fleece weight, fiber diameter, staple length (moderate to high h²: 0.30-0.60)
   - **Maternal traits**: Milk production, mothering ability (low to moderate h²)
   - **Adaptation**: Parasite resistance, heat tolerance, feet/leg soundness (low to moderate h²)
4. **Genetic evaluation**:
   - LAMBPLAN (Australia): EBVs for growth, carcass, reproduction, wool
   - NSIP (US): National Sheep Improvement Program
   - EBVs and selection indices
5. **Crossbreeding systems**:
   - Terminal sire × maternal breed ewes (most common in meat production)
   - Crossbred ewes (heterosis for reproduction and survival)
   - Rotational systems less common than in beef or swine
6. **Reproductive technologies**:
   - AI less widespread than in cattle (more challenging)
   - Estrus synchronization for seasonal breeding
   - Emerging: genomic selection, gene editing (e.g., polled allele)
7. **Challenges and opportunities**:
   - Parasite resistance (internal parasites, especially in humid climates)
   - Reproductive rate improvement (litter size, out-of-season breeding)
   - Adaptation to diverse environments
   - Declining wool prices in some regions (shift to meat emphasis)

**Learning objectives**:
- Describe breed types and their distinct breeding objectives
- Identify key traits and genetic parameters in sheep
- Explain the role of terminal sire crossbreeding in lamb production
- Understand genetic evaluation systems (LAMBPLAN, NSIP)
- Recognize challenges unique to sheep breeding (seasonal reproduction, parasite resistance)

**Examples**:
- Merino breeding for fine wool production
- Suffolk terminal sire selection for market lamb production
- LAMBPLAN EBVs for Maternal Plus index vs. Terminal Sire index
- Case study: Improving parasite resistance in hair sheep

**R demonstrations**:
- Calculate EBVs for growth and reproduction in sheep
- Simulate terminal sire crossbreeding system
- Compare economic weights for wool vs. meat production
- Estimate response to selection for litter size (low h²)

**Interactive elements**:
- Sheep crossbreeding system simulator
- Wool vs. meat breeding objective calculator

**Key messages**:
- Sheep breeding objectives vary widely (wool, meat, dual-purpose)
- Terminal sire crossbreeding is widely used in meat production
- Parasite resistance is an important selection trait in many regions
- Genetic evaluation systems exist but adoption varies by region

---

### Chapter 20: Camelidae Breeding

**Purpose**: Introduction to breeding alpacas, llamas, and camels (emerging livestock species)

**Key topics**:
1. **Camelidae species overview**:
   - **Alpacas** (Vicugna pacos): Fiber production (Huacaya and Suri types)
   - **Llamas** (Lama glama): Pack animals, fiber, guard animals
   - **Camels**: Dromedary (one hump, Arabia/Africa) and Bactrian (two humps, Central Asia)
   - Domestication history and global distribution
2. **Alpaca breeding**:
   - **Primary objective**: Fiber quality and quantity
   - **Key traits**: Fiber fineness (micron), fleece weight, fiber length, crimp, uniformity
   - **Heritabilities**: Moderate to high for fiber traits (h² ≈ 0.30-0.60)
   - **Other traits**: Conformation, temperament, reproductive efficiency
   - **Breed registries**: Limited pedigree data and genetic evaluation
   - **Color genetics**: Wide range of colors, inheritance patterns
3. **Llama breeding**:
   - **Objectives**: Temperament, size, conformation, fiber (secondary)
   - **Uses**: Packing, guarding (sheep/goat flocks), fiber, companionship
   - **Genetic evaluation**: Informal, limited structured breeding programs
4. **Camel breeding**:
   - **Objectives**: Milk production, meat, racing (specialized lines), fiber (Bactrian)
   - **Traits**: Milk yield, racing performance, body size, conformation
   - **Heritabilities**: Limited research, estimates vary widely
   - **Breeding structure**: Largely traditional, some structured breeding (racing camels)
5. **Reproductive biology**:
   - Induced ovulation (breeding season less constrained)
   - Long gestation (~11-12 months)
   - Single offspring (twins rare)
   - Challenges: Reproductive efficiency relatively low
6. **Genetic evaluation**:
   - Limited formal genetic evaluation systems
   - Some breed associations maintain registries
   - Phenotypic selection dominates
   - Opportunity for implementing modern breeding tools
7. **Challenges and opportunities**:
   - Small populations (especially alpacas outside South America)
   - Limited phenotypic data and genetic research
   - Inbreeding risk in closed populations
   - Opportunity for genomic tools to accelerate progress

**Learning objectives**:
- Describe the main camelidae species and their uses
- Identify key traits for alpaca fiber production
- Understand the challenges of breeding in small, closed populations
- Recognize opportunities for applying modern breeding methods

**Examples**:
- Alpaca fiber quality evaluation (micron, fleece weight)
- Selection for racing performance in dromedary camels
- Managing inbreeding in small alpaca herds
- Color genetics in alpacas

**R demonstrations**:
- Simulate selection for fiber fineness in alpacas
- Calculate inbreeding in small camelidae populations
- Estimate genetic trends with limited data

**Interactive elements**:
- Alpaca fiber breeding simulator
- Inbreeding calculator for small populations

**Key messages**:
- Camelidae breeding is less developed than traditional livestock
- Fiber quality is the primary objective for alpacas
- Small population sizes create genetic diversity challenges
- Opportunity exists for modern breeding methods (genomics, BLUP)

---

### Chapter 21: Aquaculture Breeding

**Purpose**: Introduce aquaculture breeding with sections on major species (salmon, trout, shrimp)

**Key topics**:
1. **Aquaculture industry overview**:
   - Fastest-growing animal protein sector globally
   - Major species: Atlantic salmon, rainbow trout, tilapia, catfish, carp, shrimp
   - Industry structure: Integration varies by species and region
   - Major breeding companies (e.g., Benchmark Genetics, SalmoBreed, Hendrix Genetics Aquaculture)
2. **Unique features of aquaculture breeding**:
   - **High fecundity**: Thousands to millions of offspring per female
   - **External fertilization**: Enables family-based selection designs
   - **Common environment**: Families can be reared together with DNA-based parentage assignment
   - **Rapid generation intervals**: 2-4 years for most species
   - **Disease challenges**: Infectious diseases major concern

**Section A: Salmon Breeding**

**Key topics**:
1. **Atlantic salmon breeding**:
   - **Key traits and heritabilities**:
     - **Growth**: Body weight at harvest (moderate to high h²: 0.25-0.40)
     - **Disease resistance**: IPN, ISA, sea lice resistance (low to moderate h²: 0.10-0.30)
     - **Flesh quality**: Color, fat content, texture (moderate h²: 0.20-0.40)
     - **Sexual maturation**: Delayed maturation desirable (moderate h²: 0.30-0.50)
     - **Deformities**: Spinal deformities, jaw malformations (low to moderate h²)
   - **Selection objectives**: Growth, disease resistance, flesh quality, delayed maturation
   - **Family-based selection**: Mixed families, DNA parentage assignment
   - **Genomic selection**: Implemented ~2010, increased accuracy and reduced generation interval
2. **Breeding structure**:
   - Closed nucleus breeding programs
   - Multiplication and grow-out stages
   - International genetics trade (eggs)
3. **Challenges**:
   - Sea lice and infectious diseases
   - Balancing growth with flesh quality
   - Inbreeding management in closed populations

**Section B: Rainbow Trout Breeding**

**Key topics**:
1. **Key traits**:
   - Growth rate (high h²: 0.30-0.50)
   - Disease resistance (variable h²: 0.10-0.40 depending on disease)
   - Flesh quality (color, texture)
   - Feed efficiency (moderate h²)
2. **Selection programs**:
   - Family-based selection
   - Some genomic selection implementation
3. **Market segmentation**:
   - Food fish (large size)
   - Sport fish (stocking programs)
   - Different breeding objectives

**Section C: Shrimp Breeding**

**Key topics**:
1. **Pacific white shrimp (Litopenaeus vannamei)**:
   - Dominant farmed shrimp species globally
   - **Key traits and heritabilities**:
     - **Growth**: Body weight at harvest (moderate h²: 0.20-0.40)
     - **Survival**: General survival, disease resistance (low to moderate h²: 0.10-0.25)
     - **Disease resistance**: Viral diseases (WSSV, TSV, IMNV) (low h²: 0.05-0.20)
     - **Reproduction**: Fecundity, mating success (low h²)
2. **Breeding structure**:
   - SPF (Specific Pathogen Free) lines
   - Family-based selection with DNA parentage
   - Genomic selection emerging
3. **Challenges**:
   - Viral disease susceptibility (major constraint)
   - Domestication relatively recent (~40 years)
   - Environmental sensitivity (salinity, temperature)

**Learning objectives**:
- Describe the unique features of aquaculture breeding (high fecundity, family-based designs)
- Identify key traits for salmon, trout, and shrimp
- Explain the role of family-based selection and genomic tools
- Understand disease resistance as a major selection objective
- Recognize the importance of DNA-based parentage assignment

**Examples**:
- Atlantic salmon family-based selection program
- Genomic selection for disease resistance in salmon
- SPF shrimp breeding program
- Case study: Genetic improvement for sea lice resistance

**R demonstrations**:
- Simulate family-based selection (full-sib families, pedigree reconstruction)
- Calculate EBVs with DNA parentage data
- Estimate response to selection for disease resistance
- Compare family selection vs. individual selection

**Interactive elements**:
- Family-based selection simulator
- Disease challenge testing visualizer

**Key messages**:
- Aquaculture breeding exploits high fecundity and family structures
- Disease resistance is critical in aquaculture breeding programs
- Genomic selection is increasingly adopted in major species
- Family-based selection with DNA parentage enables accurate breeding values

---

### Chapter 22: Companion Animal Breeding

**Purpose**: Overview of dog and cat breeding with emphasis on genetic health and breed standards

**Key topics**:
1. **Companion animal breeding context**:
   - Breeding objectives differ from livestock (aesthetics, behavior, health vs. production)
   - Breed standards and kennel clubs
   - Show breeding vs. working/performance breeding
   - Ethical considerations and welfare
2. **Dog breeding**:
   - **Breed diversity**: 200+ recognized breeds (size, conformation, behavior vary enormously)
   - **Breeding objectives**:
     - Conformation to breed standard (show dogs)
     - Performance traits (working dogs: herding, hunting, service, detection)
     - Temperament and behavior (companionship, trainability)
     - Health and longevity
   - **Key traits**:
     - **Conformation**: Size, coat color, ear shape, tail type (high h²: 0.40-0.80 for many traits)
     - **Behavior**: Aggression, fearfulness, trainability (low to moderate h²: 0.10-0.40)
     - **Performance**: Herding ability, hunting drive, endurance (moderate h²)
     - **Health**: Hip dysplasia, elbow dysplasia, eye disorders, cardiac conditions (low to moderate h²)
   - **Genetic diseases**:
     - Many breeds affected by inherited disorders
     - DNA testing available for many conditions (single gene or major genes)
     - Examples: PRA (progressive retinal atrophy), DM (degenerative myelopathy), vWD (von Willebrand disease)
   - **Inbreeding and population structure**:
     - Many breeds have limited effective population size
     - Inbreeding depression: reduced litter size, increased disease, shorter lifespan
     - Coefficient of inbreeding (COI) awareness
   - **Genomic tools**:
     - Canine SNP arrays available
     - Genomic estimated breeding values (GEBVs) for health traits
     - Parentage verification and diversity monitoring
3. **Cat breeding**:
   - **Breed diversity**: ~70 recognized breeds, but less structured than dogs
   - **Breeding objectives**:
     - Conformation to breed standards
     - Coat color, pattern, length
     - Temperament (docility, sociability)
     - Health
   - **Key traits**:
     - **Conformation and coat**: High h² for many traits
     - **Behavior**: Moderate h² for temperament traits
     - **Health**: Polycystic kidney disease (PKD), hypertrophic cardiomyopathy (HCM)
   - **Genetic testing**: Available for some conditions (PKD in Persians, etc.)
4. **Ethical and welfare considerations**:
   - Breeding for extreme conformation (brachycephalic breeds, giant breeds)
   - Health vs. aesthetics trade-offs
   - Puppy mills and unethical breeding practices
   - Responsible breeding guidelines (OFA, health testing)
5. **Breeding strategies**:
   - Limited use of quantitative genetic methods
   - Pedigree-based selection (avoiding close relatives)
   - DNA testing for single-gene disorders
   - Emerging: Genomic selection for complex health traits (hip dysplasia)
6. **Kennel clubs and registries**:
   - AKC, UKC, FCI, CFA (cats)
   - Breed standards and conformation judging
   - Health testing requirements (varies by club and breed)

**Learning objectives**:
- Describe unique features of companion animal breeding
- Identify major genetic disorders in dogs and cats
- Explain the role of DNA testing in reducing disease prevalence
- Understand inbreeding concerns in closed breed populations
- Recognize ethical considerations in companion animal breeding

**Examples**:
- Hip dysplasia in Labrador Retrievers (OFA scoring, EBVs)
- Progressive retinal atrophy (PRA) DNA testing in multiple breeds
- Reducing brachycephalic syndrome through breeding decisions
- Managing inbreeding in rare dog breeds

**R demonstrations**:
- Calculate coefficient of inbreeding (COI) from pedigrees
- Simulate selection against genetic disease (reducing allele frequency)
- Estimate effective population size in closed breeds
- Visualize pedigree relationships

**Interactive elements**:
- Inbreeding calculator (pedigree input, COI output)
- Genetic disease frequency simulator (selection, genetic testing)

**Key messages**:
- Companion animal breeding emphasizes health, temperament, and conformation
- Many breeds suffer from inbreeding and genetic disease burden
- DNA testing enables elimination of single-gene disorders
- Ethical breeding prioritizes health and welfare over extreme aesthetics
- Modern genomic tools can improve health in companion animals

---

## PART 7: PRECISION LIVESTOCK FARMING

### Chapter 23: Introduction to Precision Livestock Farming

**Purpose**: Overview of precision livestock farming (PLF) technologies and their role in phenotyping for animal breeding

**Key topics**:
1. **What is Precision Livestock Farming (PLF)?**:
   - Definition: Using sensors, automation, and data analytics to monitor and manage individual animals
   - Objectives: Improve animal welfare, productivity, efficiency, and sustainability
   - Contrast with traditional management (visual observation, manual recording)
2. **PLF technologies overview**:
   - **Sensors**: Wearables, cameras, microphones, environmental sensors, feeding systems
   - **Data collection**: Continuous, automated, high-resolution
   - **Data analytics**: Machine learning, computer vision, predictive models
   - **Decision support**: Alerts, recommendations, automated actions
3. **PLF for phenotyping in animal breeding**:
   - **High-throughput phenotyping**: Measure thousands of animals automatically
   - **New traits**: Traits difficult or expensive to measure traditionally (individual feed intake, activity, behavior)
   - **Precision**: Reduced measurement error compared to manual methods
   - **Longitudinal data**: Repeated measurements over time (growth curves, activity patterns)
4. **Key application areas**:
   - **Feed efficiency**: Individual feed intake (RFI, FCR)
   - **Health monitoring**: Early disease detection, lameness, mastitis
   - **Reproduction**: Estrus detection, calving/farrowing monitoring
   - **Behavior and welfare**: Activity, lying time, social interactions
   - **Growth and body composition**: Automated weighing, 3D imaging
   - **Environmental impact**: Methane emissions, nitrogen excretion
5. **Data management challenges**:
   - **Volume**: Massive datasets (terabytes per farm)
   - **Quality control**: Sensor errors, missing data, outliers
   - **Integration**: Linking sensor data with pedigree and genomic data
   - **Privacy and security**: Data ownership, sharing, security
6. **PLF and genetic improvement**:
   - Enabling selection for hard-to-measure traits (feed efficiency, methane, health)
   - Increasing accuracy of genetic evaluations (more data per animal)
   - Identifying new traits (resilience, robustness, stress response)
   - Genotype-by-environment interactions (individual animal responses to stressors)
7. **Challenges and opportunities**:
   - **Cost**: Initial investment in sensors and infrastructure
   - **Validation**: Ensuring sensor data accurately reflects biological traits
   - **Adoption**: Farmer acceptance, training, infrastructure
   - **Integration with breeding programs**: Incorporating PLF data into genetic evaluations

**Learning objectives**:
- Define precision livestock farming and its objectives
- Identify major PLF technologies and their applications
- Explain how PLF enables high-throughput phenotyping for breeding
- Understand data management challenges with PLF
- Recognize opportunities for PLF to accelerate genetic improvement

**Examples**:
- GrowSafe feed intake systems for RFI measurement in beef cattle
- Automated milking systems (AMS) for dairy cow health and production monitoring
- Ear tag accelerometers for activity and lying time in dairy cattle
- Camera-based body condition scoring
- Methane measurement using sniffer devices

**R demonstrations**:
- Visualize feed intake data from automated feeders
- Calculate RFI from individual feed intake and growth data
- Analyze activity patterns from accelerometer data
- Quality control for sensor data (detect outliers, impute missing values)

**Interactive elements**:
- PLF data explorer (visualize sensor data streams)
- RFI calculator using automated feed intake data

**Key messages**:
- Precision livestock farming enables automated, high-throughput phenotyping
- PLF technologies generate vast amounts of data requiring careful management
- PLF enables genetic selection for traits previously too expensive to measure
- Integration of PLF data with breeding programs is an active research area

---

### Chapter 24: Wearable Technologies in Livestock

**Purpose**: Detailed examination of wearable sensors (collars, ear tags, leg bands) for monitoring livestock

**Key topics**:
1. **Types of wearable sensors**:
   - **Collars**: Accelerometers, GPS, microphones, body temperature sensors
   - **Ear tags**: RFID (identification), accelerometers, temperature sensors
   - **Leg bands**: Accelerometers, pedometers (step counting)
   - **Rumen boluses**: pH, temperature, pressure (ruminants)
   - **Subcutaneous sensors**: Temperature, physiological parameters (research/specialized)
2. **Accelerometers and activity monitoring**:
   - **Measured parameters**: Activity level, lying time, standing time, step count, rumination time
   - **Applications**:
     - **Estrus detection**: Increased activity during estrus (dairy cows)
     - **Calving/farrowing detection**: Changes in lying patterns before parturition
     - **Lameness detection**: Reduced activity, altered gait, increased lying time
     - **Health monitoring**: Reduced activity as early indicator of disease
     - **Welfare assessment**: Lying time, rumination time as welfare indicators
   - **Data analytics**: Machine learning models to classify behaviors
   - **Commercial systems**: Allflex, SCR by Allflex, IceQube, RumiWatch, Nedap
3. **Temperature sensors**:
   - **Core body temperature**: Early indicator of fever, heat stress
   - **Applications**:
     - Disease detection (fever)
     - Heat stress monitoring
     - Estrus detection (temperature changes)
   - **Rumen boluses**: Continuous temperature and pH monitoring
4. **GPS and location tracking**:
   - **Grazing behavior**: Pasture utilization, grazing patterns
   - **Extensive systems**: Locating animals in large pastures or rangeland
   - **Behavior research**: Social interactions, resource use
5. **Acoustic sensors (microphones)**:
   - **Cough detection**: Respiratory disease monitoring (swine, cattle)
   - **Vocalization analysis**: Stress, pain, estrus
   - **Rumination detection**: Using neck-mounted microphones
6. **Wearables for genetic evaluation**:
   - **Feed efficiency**: Activity data helps explain variation in energy expenditure
   - **Health traits**: Early disease detection enables phenotyping for resistance
   - **Fertility**: Improved estrus detection increases accuracy of fertility EBVs
   - **Temperament**: Activity patterns indicate stress response
7. **Data quality and validation**:
   - Comparing sensor data to gold-standard measurements
   - Calibration and drift correction
   - Battery life and maintenance
   - Missing data due to sensor failure or loss
8. **Challenges**:
   - Cost per animal (especially for large herds)
   - Battery life and replacement
   - Data management infrastructure
   - Validation of sensor accuracy

**Learning objectives**:
- Identify major types of wearable sensors and their applications
- Explain how accelerometers are used for estrus detection and health monitoring
- Understand how wearable data can be used in genetic evaluations
- Recognize challenges in deploying wearable technologies
- Interpret activity and behavior data from wearable sensors

**Examples**:
- Allflex SenseHub dairy collar for estrus detection and health monitoring
- IceQube leg sensor for lameness detection in dairy cows
- Rumen boluses for pH monitoring in feedlot cattle
- GPS collars for grazing behavior in extensive beef systems

**R demonstrations**:
- Analyze accelerometer data (activity patterns, detect estrus events)
- Visualize lying time and rumination time over days
- Build a simple classifier for lameness using activity data
- Calculate heritability of activity traits
- Estimate genetic correlations between activity and production traits

**Interactive elements**:
- Activity pattern visualizer (input sensor data, visualize daily patterns)
- Estrus detection algorithm demonstrator

**Key messages**:
- Wearable sensors enable continuous, automated monitoring of behavior and physiology
- Accelerometers are widely adopted for estrus and health detection
- Wearable data provides novel phenotypes for genetic evaluation
- Data quality and validation are critical for reliable use

---

### Chapter 25: Computer Vision and Camera Technologies

**Purpose**: Explore camera-based phenotyping using 2D and 3D imaging and computer vision

**Key topics**:
1. **Introduction to computer vision in livestock**:
   - Using cameras and image analysis to extract phenotypic information
   - Advantages: Non-invasive, high-throughput, automated
   - Types: 2D cameras (RGB), 3D cameras (depth sensors, stereo cameras, LiDAR), thermal cameras
2. **2D image analysis**:
   - **Applications**:
     - **Body condition scoring (BCS)**: Automated scoring using images of animals (dairy, beef)
     - **Activity and behavior**: Posture classification, social interactions, feeding behavior
     - **Lameness detection**: Gait analysis from video
     - **Identification**: Facial recognition, coat pattern identification
   - **Computer vision techniques**:
     - Object detection (locate animals in images)
     - Image segmentation (separate animal from background)
     - Feature extraction (body shape, posture)
     - Deep learning (convolutional neural networks for classification and regression)
   - **Commercial systems**: DeLaval body condition scoring, Cainthus (behavior monitoring)
3. **3D imaging and depth sensors**:
   - **Technologies**: Time-of-flight cameras, structured light, stereo vision, LiDAR
   - **Applications**:
     - **Body weight estimation**: 3D body volume correlates with weight
     - **Body composition**: Estimate muscle and fat distribution
     - **Growth monitoring**: Automated weight tracking without handling animals
     - **Conformation traits**: Measure body dimensions (height, length, chest girth)
   - **Systems**: Cattle (3D cameras at milking parlor or feeding station), swine (3D cameras at entry/exit)
   - **Accuracy**: High correlation with manual measurements (r > 0.90 for weight in many systems)
4. **Thermal imaging**:
   - **Applications**:
     - **Health monitoring**: Elevated body temperature indicates fever or inflammation
     - **Heat stress detection**: Monitor heat load in animals
     - **Mastitis detection**: Udder temperature changes
   - **Challenges**: Environmental factors affect measurements (ambient temperature, humidity)
5. **Video analysis for behavior**:
   - **Eating and drinking**: Time spent at feeder/drinker, feeding rate
   - **Social interactions**: Aggression, mounting, grooming
   - **Lying and standing behavior**: Posture classification
   - **Gait analysis**: Lameness scoring from video
   - **Farrowing/calving monitoring**: Detect parturition events
   - **Machine learning**: Train models to classify behaviors from video
6. **Computer vision for genetic evaluation**:
   - **Body composition traits**: 3D imaging provides accurate carcass predictions (live animal)
   - **Feed efficiency**: Video analysis of feeding behavior
   - **Health traits**: Early disease detection (gait, posture, activity)
   - **Conformation**: Automated measurement of body dimensions
   - **Welfare traits**: Behavior-based indicators (fear response, social stress)
7. **Challenges**:
   - **Environmental variability**: Lighting, dust, occlusions
   - **Computational requirements**: Processing large video datasets
   - **Model training**: Requires labeled data (ground truth)
   - **Generalization**: Models trained on one farm may not work on another
   - **Cost**: High-resolution cameras, computing infrastructure
8. **Future directions**:
   - Integration with genomic data (genotype-by-environment, resilience)
   - Real-time alerts for health and welfare issues
   - Scaling to commercial farms
   - Multi-modal sensing (combine video, wearables, environmental sensors)

**Learning objectives**:
- Describe types of cameras used in livestock monitoring (2D, 3D, thermal)
- Explain how computer vision is used for body condition scoring and weight estimation
- Understand the role of machine learning in video analysis
- Identify applications of camera-based phenotyping for genetic evaluation
- Recognize challenges in deploying computer vision on commercial farms

**Examples**:
- Automated body condition scoring in dairy cows using 2D cameras
- 3D camera system for weighing pigs at entry to finishing barn
- Lameness detection from gait analysis (video + deep learning)
- Thermal imaging for mastitis detection in dairy cows
- Facial recognition for individual animal identification

**R demonstrations**:
- Analyze body weight data from 3D imaging system (growth curves)
- Calculate heritability of video-derived traits (lying time, feeding rate)
- Estimate genetic correlations between video traits and production traits
- Visualize body condition scores over time (lactation curve for dairy)
- Build a simple linear model predicting body weight from 3D measurements

**Interactive elements**:
- 3D body weight estimator (input body dimensions, predict weight)
- Body condition score classifier (upload image, predict BCS)

**Key messages**:
- Computer vision enables non-invasive, high-throughput phenotyping
- 3D imaging accurately estimates body weight and composition
- Machine learning is critical for analyzing video and image data
- Camera-based phenotyping provides novel traits for genetic selection
- Integration with breeding programs is expanding rapidly

---

## Appendices

### Appendix A: Datasets

**Purpose**: Document all datasets used in the book

**Content**:
- Dataset name, file path, and description
- Variables and units
- Sample size and structure
- Source or simulation parameters
- Example use in which chapter(s)

**Example entry**:
```
Dataset: swine_growth_heritability.csv
Location: data/swine_growth_heritability.csv
Description: Simulated growth data for 500 pigs from 50 litters
Variables:
  - pig_id: Unique pig identifier
  - sire_id: Sire identifier
  - dam_id: Dam identifier
  - litter_id: Litter identifier
  - birth_wt: Birth weight (kg)
  - weaning_wt: Weaning weight (kg, 21 days)
  - final_wt: Final weight (kg, 150 days)
Simulation parameters: h² = 0.30, σ²_P = 100 kg²
Used in: Chapter 5 (heritability), Chapter 6 (breeder's equation)
```

### Appendix B: R Resources

**Purpose**: Guide students to R packages and resources for animal breeding

**Content**:
- **Core packages**:
  - tidyverse (data manipulation, plotting)
  - pedigree (pedigree processing)
  - AGHmatrix (relationship matrices)
  - MCMCglmm, brms, bglr (Bayesian models)
  - nadiv (pedigree-based genetic evaluation)
- **Specialized packages**:
  - AlphaSimR (stochastic simulation of breeding programs)
  - BGLR (genomic prediction)
  - rrBLUP (genomic prediction)
- **Online resources**:
  - Beef Improvement Federation guidelines
  - National Swine Improvement Federation resources
  - Dairy cattle genomic evaluation documentation (CDCB)
- **Textbooks and references**:
  - Falconer and Mackay, *Introduction to Quantitative Genetics*
  - Lynch and Walsh, *Genetics and Analysis of Quantitative Traits*
  - Mrode, *Linear Models for the Prediction of Animal Breeding Values*
  - Gianola and Fernando papers on Bayesian methods

### Appendix C: Glossary (Optional)

**Purpose**: Quick reference for genetic terminology

**Content**: Alphabetical list of key terms with concise definitions

**Example entries**:
- **Additive genetic variance (σ²_A)**: Variance in breeding values in a population
- **Breeding value (BV)**: Sum of average effects of an individual's alleles; determines genetic merit as a parent
- **EBV (Estimated Breeding Value)**: Statistical prediction of an animal's true breeding value
- **Heritability (h²)**: Proportion of phenotypic variance due to additive genetic effects
- **Heterosis**: Superiority of crossbred offspring over purebred parents
- **BLUP**: Best Linear Unbiased Prediction; method for estimating breeding values

---

## Final Notes

### Development Workflow

1. **Draft chapter structure**: Create outline with section headings
2. **Write conceptual content**: Explain concepts in plain language first
3. **Add equations and math**: Present mathematical formulations with careful notation
4. **Develop examples**: Create realistic livestock examples with step-by-step solutions
5. **Write R code**: Implement calculations, simulations, visualizations
6. **Review and revise**: Ensure accuracy, clarity, and pedagogical flow
7. **Add interactive elements** (later stage): Develop Shiny apps or widgets

### Collaboration and Feedback

- **Peer review**: Have colleagues review chapters for accuracy and clarity
- **Student testing**: Pilot chapters with undergraduate students to identify confusing sections
- **Industry input**: Engage breeding company geneticists for real-world relevance

### Maintenance and Updates

- **Annual reviews**: Update examples, data, and company information
- **Software updates**: Ensure R code works with latest package versions
- **Genomic advances**: Update Chapters 12-13 as genomic methods evolve
- **Literature**: Add references to recent papers and reviews

---

## Questions or Suggestions?

This guide is a living document. As the textbook develops, update this file to reflect new decisions, lessons learned, and improvements. If you have questions about any aspect of the book development, consult this guide first, then discuss with the development team.

**Good luck, and happy writing!**
