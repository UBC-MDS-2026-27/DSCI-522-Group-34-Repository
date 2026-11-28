# Predicting Extra Paid Mathematics Classes from Student Background

**Authors:** Chengyan Zhao, Vikasini Senthilkumar, Shorya Jain, Arunark Singh

This project was completed for DSCI 522 (Data Science Workflows), a course in the Master of Data Science program at the University of British Columbia.

**Rendered report:** <https://ubc-mds-2026-27.github.io/DSCI-522-Group-34-Repository/analysis/predicting-paid-math-classes.html>

## Summary

We asked whether students' family backgrounds and study-related characteristics can predict whether they attend extra paid mathematics classes. Using records for 395 students at two Portuguese secondary schools, we compared logistic regression, a shallow decision tree and a random forest with five-fold cross-validation. Logistic regression performed best, with a mean validation accuracy of 64.2%. On the held-out test set it reached 58.6% accuracy, only modestly above the 54.5% achieved by always predicting the most common outcome. This suggests that family background and study habits carry some information about who attends paid classes, but not enough to predict reliably for an individual student. The data cover only two schools, the predictors leave out factors such as family income and a student's reasons for seeking extra help, and the results describe associations rather than causes.

## Data

We use the mathematics file of the *Student Performance* data set (Cortez, 2008), available from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/320/student+performance) under a [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) license. It contains 395 students from two Portuguese secondary schools, collected through school reports and questionnaires, with one row per student. Our response variable is whether a student attended extra paid mathematics classes (yes or no). Our predictors are parents' education and occupations, family size, parents' cohabitation status, weekly study time, past class failures, family educational support, school, and home address type. We exclude the three period grades because they may already reflect tutoring participation.

The report downloads the data into `data/raw/` each time it is rendered, and writes the cleaned data and the train/test split to `data/processed/`.

## Usage

We run the analysis in a Docker container so everyone uses the same software and package versions. The image is avaliable on [Docker Hub](https://hub.docker.com/r/arunark3/dsci-522-group-34-repository).

Install and launch [Docker Desktop](https://www.docker.com/get-started/). Clone the repository and move into it.

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-34-Repository.git
cd DSCI-522-Group-34-Repository
```

Run the following commands from the repository root.

### 1. Create an SSH key

If you do not already have an Ed25519 SSH key at the default location, run the following command and press Enter at each prompt.

```bash
ssh-keygen -t ed25519
```

If the public key is missing when you first run the container, Docker can create a directory named `~/.ssh/id_ed25519.pub`. If that ever happens, remove the directory and run `ssh-keygen` before trying to connect to the container over SSH. 

### 2. Download the Docker image

```bash
docker compose pull
```

### 3. Run the analysis and reder the report

```bash
docker compose run --rm analysis-env uv run quarto render analysis/predicting-paid-math-classes.qmd
```

Rendering downloads the data from the UCI Mahine Learning Repository, so it will requires a internet connection. Open `analysis/predicting-paid-math-classes.html` in your browser to view the report.

The `--rm` option automatically removes the container when rendering finishes. 

## Contributing

We welcome contributions. Please read [CONTRIBUTING.md](CONTRIBUTING.md) and follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## Dependencies

- R 4.6 with the packages pinned in [`renv.lock`](renv.lock), mainly tidyverse, reticulate, rmarkdown and knitr.
- Python 3.14 with the packages listed in [`pyproject.toml`](pyproject.toml) and pinned in [`uv.lock`](uv.lock): pandas, scikit-learn, Altair, ipykernel, nbformat, nbclient, PyYAML and tabulate.
- [uv](https://docs.astral.sh/uv/), [renv](https://rstudio.github.io/renv/) and [Quarto](https://quarto.org/).
- The Docker image is built from the [`Dockerfile`](Dockerfile), which installs the software and packages needed to run the analysis.

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

## References

Cortez, P. (2008). *Student Performance* [Data set]. UCI Machine Learning Repository. <https://doi.org/10.24432/C5TG7T>

Cortez, P., & Silva, A. M. G. (2008). Using data mining to predict secondary school student performance. In *Proceedings of the 5th Annual Future Business Technology Conference* (pp. 5–12). EUROSIS.