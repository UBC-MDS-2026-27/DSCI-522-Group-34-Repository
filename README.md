# Predicting Secondary School Student Performance

**Authors:** Chengyan Zhao, Vikasini Senthilkumar, Shorya Jain, Arunark Singh

This project was completed for DSCI 522 (Data Science Workflows), a course in the Master of Data Science program at the University of British Columbia.

**Rendered report:** <https://ubc-mds-2026-27.github.io/DSCI-522-Group-34-Repository/analysis/[TODO: report-name].html>

## Summary

[TODO: Write once the analysis is done. One paragraph covering: the question you asked, the model you used, the main result with its metric (for example, test RMSE or F1), the strongest predictors, and one or two sentences on what the findings mean and their main limitations.]

## Data

We use the *Student Performance* data set (Cortez, 2008), available from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/dataset/320/student+performance) under a [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) license. It records the achievement of students at two Portuguese secondary schools, collected from school reports and questionnaires. The data include each student's grades along with demographic, social and school-related information. There are two files, one for Mathematics and one for Portuguese language. Each row is one student, and grades are on a 0 to 20 scale over three periods (G1, G2 and the final grade G3).

[TODO: State which file(s) you use and what you predict, for example: "We use the Portuguese language file (649 students) and predict the final grade G3 without using the first- and second-period grades G1 and G2."]

The analysis downloads the data automatically into `data/raw/` the first time the report is rendered, and writes the cleaned version to `data/processed/`.

## How to run the analysis

You need two programs installed on your computer:

- [uv](https://docs.astral.sh/uv/getting-started/installation/) (version 0.5 or later), which installs Python and all the packages listed in `pyproject.toml`; and
- [Quarto](https://quarto.org/docs/get-started/) (version 1.6 or later), which renders the report.

You can check that both are installed by running `uv --version` and `quarto --version` in a terminal.

**1. Clone the repository and move into it.**

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-34-Repository.git
cd DSCI-522-Group-34-Repository
```

**2. Create the environment.** This installs the exact package versions recorded in `uv.lock` into a folder called `.venv`. If the right version of Python is not on your computer, uv downloads it.

```bash
uv sync
```

**3. Activate the environment.** Quarto needs to use the Python inside `.venv`, so activate it before rendering. Use the command for your system:

| System and terminal | Command |
|---|---|
| macOS or Linux | `source .venv/bin/activate` |
| Windows, Git Bash | `source .venv/Scripts/activate` |
| Windows, PowerShell | `.venv\Scripts\activate` |

**4. Render the report.** This downloads the data (if it is not already in `data/raw/`), runs the full analysis and writes the HTML report.

```bash
quarto render analysis/[TODO: report-name].qmd
```

Open `analysis/[TODO: report-name].html` in a web browser to read the report. Rendering takes under a minute on a typical laptop and needs an internet connection. When you are finished, you can leave the environment with `deactivate`.

## Dependencies

- [uv](https://docs.astral.sh/uv/) and [Quarto](https://quarto.org/)
- Python 3.13 and the packages listed in [`pyproject.toml`](pyproject.toml), with exact versions pinned in [`uv.lock`](uv.lock): pandas, scikit-learn, Altair, ipykernel, nbformat, nbclient, PyYAML and tabulate.

## Repository structure

```
.
├── README.md
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── LICENSE.md
├── pyproject.toml, uv.lock, .python-version   # computational environment
├── data/
│   ├── raw/          # data exactly as downloaded from UCI
│   └── processed/    # cleaned data used in the analysis
└── analysis/
    ├── [TODO: report-name].qmd    # report source
    ├── [TODO: report-name].html   # rendered report
    └── references.bib             # bibliography
```

## Licenses

- The code in this project is licensed under the **MIT License**.
- The report is licensed under the **Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License (CC BY-NC-ND 4.0)**.

See [LICENSE.md](LICENSE.md) for the full text of both licenses. The data set is licensed separately by its author under CC BY 4.0.

## AI use statement

We used generative AI in this project. [TODO: Edit this section so it accurately describes how your team used AI.]

Claude (Anthropic) was used to help draft the README, CODE_OF_CONDUCT and CONTRIBUTING files and parts of the analysis code. All team members reviewed, edited and tested this material, checked every reference against its original source, and are responsible for the final content. No instruction files (such as a `CLAUDE.md`) were used. Issues, pull requests and reviews in this repository were created by team members, not by AI tools.

Example prompts:

- "Update our README for the UCI Student Performance data set, our team members and our repository link."
- "Review this CONTRIBUTING.md and suggest an AI policy section consistent with a course that requires human-opened pull requests."

## Contributing

We welcome contributions. Please read [CONTRIBUTING.md](CONTRIBUTING.md) and follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## References

Cortez, P. (2008). *Student Performance* [Data set]. UCI Machine Learning Repository. <https://doi.org/10.24432/C5TG7T>

Cortez, P., & Silva, A. M. G. (2008). Using data mining to predict secondary school student performance. In *Proceedings of the 5th Annual Future Business Technology Conference* (pp. 5–12). EUROSIS.