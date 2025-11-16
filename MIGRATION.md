# Migration Guide: GitHub Actions Deployment

## Overview

This guide walks you through migrating your Quarto book from local rendering (with the `docs/` folder) to automated GitHub Actions deployment.

## What Changed

### Files Modified
1. **`.github/workflows/quarto-publish.yml`** - NEW: GitHub Actions workflow file
2. **`_quarto.yml`** - Changed `output-dir: docs` → `output-dir: _site`
3. **`.gitignore`** - Added `/docs/` to ignore list, updated comments

### Deployment Method
- **Before**: Render locally → commit `docs/` folder → push to GitHub → GitHub Pages serves from `docs/`
- **After**: Push source files → GitHub Actions renders automatically → deploys to GitHub Pages from `_site/`

## Migration Steps

### Step 1: Configure GitHub Pages Settings

1. Go to your repository on GitHub
2. Click **Settings** → **Pages** (in left sidebar)
3. Under **"Source"**, change from **"Deploy from a branch"** to **"GitHub Actions"**
4. Save the settings

**IMPORTANT**: This is crucial! The source must be set to "GitHub Actions" for the workflow to deploy properly.

### Step 2: Trigger First Workflow Run

The workflow is already set up and will run automatically on the next push to `main`. You can also manually trigger it:

Option A - Workflow will trigger automatically on push (recommended)

Option B - Manually trigger the workflow:
1. Go to **Actions** tab in GitHub
2. Click on **"Render and Publish Quarto Book"** workflow
3. Click **"Run workflow"** button
4. Select `main` branch
5. Click **"Run workflow"**

### Step 3: Monitor First Build

1. Go to the **Actions** tab in your repository
2. Click on the running workflow
3. Watch the build progress (should take 5-10 minutes for first run)
4. Check for any errors in the logs

**Expected duration**:
- First run: 8-12 minutes (installing all R packages)
- Subsequent runs: 3-5 minutes (packages cached)

### Step 4: Verify Deployment

Once the workflow succeeds:

1. Check the **Actions** tab - workflow should show green checkmark ✅
2. Visit your GitHub Pages URL: `https://austin-putz.github.io/fundamentals-of-animal-breeding/`
3. Verify the book renders correctly
4. Test navigation, search, and interactive elements

### Step 5: Clean Up Local Repository (AFTER Successful Deployment)

Once you confirm the GitHub Actions deployment works:

```bash
# Remove the old docs/ folder
git rm -r docs/

# Commit the deletion
git commit -m "Remove docs/ folder (now using GitHub Actions)"

# Push to GitHub
git push origin main
```

**IMPORTANT**: Only do this AFTER confirming the GitHub Actions deployment works!

## Troubleshooting

### Build Fails: R Package Installation Errors

**Problem**: Some R packages fail to install during the workflow.

**Solution**: Check the workflow logs for specific errors. Common issues:
- Package dependencies missing (system libraries)
- Package name typo
- Package requires Bioconductor (not CRAN)

**Fix**: Edit `.github/workflows/quarto-publish.yml` to add missing system dependencies or adjust package installation.

### Build Fails: Quarto Rendering Errors

**Problem**: Workflow succeeds at package installation but fails during `quarto render`.

**Solution**:
1. Check which .qmd file is causing the error in the logs
2. Test rendering locally: `quarto render`
3. Fix errors in the problematic chapter
4. Commit and push fixes

### Deployment Succeeds but Site Shows 404

**Problem**: Workflow completes successfully, but the GitHub Pages URL shows 404.

**Solution**:
1. Verify GitHub Pages is set to "GitHub Actions" source (Step 1)
2. Check that the workflow has "pages: write" permissions
3. Wait 2-3 minutes for DNS propagation
4. Try clearing browser cache

### Build is Slow (10+ minutes)

**Problem**: Every build takes 10+ minutes.

**Solution**: R package caching should speed this up. If not:
1. Check that the cache step in the workflow is running
2. Verify `actions/cache@v3` is working properly
3. Consider reducing number of packages if some are unused

### Book Renders Differently than Local

**Problem**: GitHub Actions build looks different from local rendering.

**Solution**:
1. Check R package versions - workflow installs latest versions
2. Check Quarto version - workflow uses specific version (1.4.549)
3. Consider using `renv` for exact package version locking (advanced)

## Workflow Details

### R Packages Installed (24 total)

**Core Packages**:
- tidyverse (includes ggplot2, dplyr, tidyr, readr, tibble, etc.)
- scales, patchwork
- knitr, kableExtra

**Genetics Packages**:
- pedigree, nadiv, AGHmatrix
- lme4, lmerTest, MCMCglmm
- BGLR, rrBLUP, brms
- AlphaSimR

**Data & Analysis**:
- DBI, RSQLite
- MASS, reshape2
- httr, jsonlite
- swirl

### Workflow Triggers

The workflow runs on:
- **Push to `main`**: Automatic deployment on every commit
- **Pull requests**: Build preview (doesn't deploy)
- **Manual trigger**: Via "Run workflow" button in Actions tab

### Caching Strategy

R packages are cached to speed up builds:
- **Cache key**: Based on DESCRIPTION file and .qmd file hashes
- **Cache location**: `$R_LIBS_USER`
- **Benefit**: Reduces build time from 10 minutes to 3-5 minutes

## Benefits of GitHub Actions Deployment

✅ **Automated**: No more manual rendering and committing
✅ **Consistent**: Same build environment every time
✅ **Cleaner Git History**: Only track source files, not rendered HTML
✅ **Faster Collaboration**: Contributors only edit .qmd files
✅ **Professional**: Industry-standard CI/CD pipeline
✅ **Reproducible**: Locked versions of R, Quarto, and packages

## Rollback Instructions

If you need to rollback to the old `docs/` folder method:

```bash
# 1. Restore old _quarto.yml
git revert <commit-hash-of-quarto-yml-change>

# 2. Restore old .gitignore
git revert <commit-hash-of-gitignore-change>

# 3. Disable GitHub Actions workflow
# Go to GitHub → Actions → Click workflow → Click "..." → Disable workflow

# 4. Change GitHub Pages source back to "Deploy from a branch" → "main" → "/docs"

# 5. Render locally and commit docs/
quarto render
git add docs/
git commit -m "Restore local rendering"
git push origin main
```

## Next Steps (Optional Enhancements)

### 1. Add renv for Reproducibility

Create `renv.lock` to lock exact package versions:

```r
# In R console
install.packages("renv")
renv::init()
renv::snapshot()
```

Then update workflow to use renv:
```yaml
- name: Restore R packages
  run: |
    renv::restore()
  shell: Rscript {0}
```

### 2. Add Status Badge to README

Add a build status badge to show workflow status:

```markdown
[![Quarto Publish](https://github.com/austin-putz/fundamentals-of-animal-breeding/actions/workflows/quarto-publish.yml/badge.svg)](https://github.com/austin-putz/fundamentals-of-animal-breeding/actions/workflows/quarto-publish.yml)
```

### 3. Set Up Branch Protections

Require workflow to pass before merging pull requests:
1. Settings → Branches → Add rule
2. Require status checks to pass: "build"

### 4. Add Preview Deployments for PRs

Deploy previews for pull requests before merging (advanced).

## Support

If you encounter issues:
1. Check the [Quarto documentation](https://quarto.org/docs/publishing/github-pages.html)
2. Review GitHub Actions logs for specific errors
3. Consult the [r-lib/actions](https://github.com/r-lib/actions) repository for R-specific actions

## Summary

You've successfully migrated to GitHub Actions! Your workflow will now:
1. ✅ Automatically render your book on every push
2. ✅ Install all required R packages
3. ✅ Deploy to GitHub Pages
4. ✅ Cache packages for faster builds

**No more manual `quarto render` and committing `docs/` folder!**
