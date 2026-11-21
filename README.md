# Predicting Extra Paid Mathematics Classes from Student Background

**Authors:** Chengyan Zhao, Vikasini Senthilkumar, Shorya Jain, Arunark Singh

This project was completed for DSCI 522 (Data Science Workflows), a course in the Master of Data Science program at the University of British Columbia.

**Rendered report:** <https://ubc-mds-2026-27.github.io/DSCI-522-Group-34-Repository/analysis/predicting-paid-math-classes.html>

## Summary

We asked whether students' family backgrounds and study-related characteristics can predict whether they attend extra paid mathematics classes. Using records for 395 students at two Portuguese secondary schools, we compared logistic regression, a shallow decision tree and a random forest with five-fold cross-validation. Logistic regression performed best, with a mean validation accuracy of 64.2%. On the held-out test set it reached 58.6% accuracy, only modestly above the 54.5% achieved by always predicting the most common outcome. This suggests that family background and study habits carry some information about who attends paid classes, but not enough to predict reliably for an individual student. The data cover only two schools, the predictors leave out factors such as family income and a student's reasons for seeking extra help, and the results describe associations rather than causes.

## Data

We use the mathematics file of the *Student Performance* data set (Cortez, 2008), available from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/320/student+performance) under a [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) license. It contains 395 students from two Portuguese secondary schools, collected through school reports and questionnaires, with one row per student. Our response variable is whether a student attended extra paid mathematics classes (yes or no). Our predictors are parents' education and occupations, family size, parents' cohabitation status, weekly study time, past class failures, family educational support, school, and home address type. We exclude the three period grades because they may already reflect tutoring participation.

The report downloads the data into `data/raw/` each time it is rendered, and writes the cleaned data and the train/test split to `data/processed/`.

## How to run the analysis

The analysis uses R for data download and cleaning, and Python (called from R through the reticulate package) for the train/test split, exploratory analysis and modelling.

**Requirements.** Install the following, then check each with the command shown:

| Program | Version | Check |
|---|---|---|
| [R](https://cran.r-project.org/) | 4.6 or later | `R --version` |
| [uv](https://docs.astral.sh/uv/getting-started/installation/) | 0.9 or later | `uv --version` |
| [Quarto](https://quarto.org/docs/get-started/) | 1.6 or later | `quarto --version` |

On Windows, run the commands below in Git Bash. If `Rscript` is not found, either add R's `bin` folder to your PATH, or open `DSCI-522-Group-34-Repository.Rproj` in RStudio and run the R commands in its Console.

**1. Clone the repository and move into it.**

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-34-Repository.git
cd DSCI-522-Group-34-Repository
```

**2. Create the Python environment.** This installs Python 3.14 (if needed) and the exact package versions in `uv.lock` into a `.venv` folder.

```bash
uv sync
```

**3. Restore the R packages.** This installs the exact R package versions recorded in `renv.lock` into a project library. The first run takes a few minutes.

```bash
Rscript -e 'renv::restore(prompt = FALSE)'
```

**4. Render the report.**

```bash
quarto render analysis/predicting-paid-math-classes.qmd
```

Open `analysis/predicting-paid-math-classes.html` in a web browser to read the report. Rendering needs an internet connection because the data are downloaded from UCI.

## Dependencies

- R 4.6 with the packages pinned in [`renv.lock`](renv.lock), mainly tidyverse, reticulate, rmarkdown and knitr.
- Python 3.14 with the packages listed in [`pyproject.toml`](pyproject.toml) and pinned in [`uv.lock`](uv.lock): pandas, scikit-learn, Altair, ipykernel, nbformat, nbclient, PyYAML and tabulate.
- [uv](https://docs.astral.sh/uv/), [renv](https://rstudio.github.io/renv/) and [Quarto](https://quarto.org/).

## Repository structure

```
.
├── README.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE.md
├── pyproject.toml, uv.lock, .python-version   # Python environment (uv)
├── renv.lock, .Rprofile, renv/                # R environment (renv)
├── DSCI-522-Group-34-Repository.Rproj         # RStudio project file
├── data/
│   ├── raw/          # data exactly as downloaded from UCI
│   └── processed/    # cleaned data and train/test split
└── analysis/
    ├── predicting-paid-math-classes.qmd    # report source
    └── predicting-paid-math-classes.html   # rendered report
```

## Licenses

- The code in this project is licensed under the **MIT License**.
- The report is licensed under the **Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License (CC BY-NC-ND 4.0)**.

See [LICENSE.md](LICENSE.md) for the full text of both licenses. The data set is licensed separately by its author under CC BY 4.0.

## AI use statement

We used generative AI in parts of this project. Claude (Anthropic) was used to help draft the README, CODE_OF_CONDUCT, CONTRIBUTING and LICENSE files, and to troubleshoot the renv and uv environment setup. 

The research question, data set choice, analysis code and report were developed by the team. No AI instruction files (such as a `CLAUDE.md`) were used. Issues, pull requests and reviews in this repository were created by team members, not by AI tools.

Example prompts:

- "Update our README for the UCI Student Performance data set, and our repository link."
- "How do I add reticulate to our renv lockfile?"

## Contributing

We welcome contributions. Please read [CONTRIBUTING.md](CONTRIBUTING.md) and follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## References

Cortez, P. (2008). *Student Performance* [Data set]. UCI Machine Learning Repository. <https://doi.org/10.24432/C5TG7T>

Cortez, P., & Silva, A. M. G. (2008). Using data mining to predict secondary school student performance. In *Proceedings of the 5th Annual Future Business Technology Conference* (pp. 5–12). EUROSIS.