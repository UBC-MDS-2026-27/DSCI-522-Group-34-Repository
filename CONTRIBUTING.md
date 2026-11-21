# Contributing to Predicting Extra Paid Mathematics Classes

Thank you for your interest in this project. We welcome bug reports, suggestions, corrections to the report and improvements to the code. This guide explains how to contribute. It is adapted from the contributing guides of [dplyr](https://github.com/tidyverse/dplyr/blob/main/.github/CONTRIBUTING.md) and [Altair](https://github.com/vega/altair/blob/main/CONTRIBUTING.md). The AI policy below is adapted from the [SymPy AI-generated code policy](https://docs.sympy.org/dev/contributing/ai-generated-code-policy.html) and the [earthaccess AI policy](https://earthaccess.readthedocs.io/en/latest/contributor/ai-policy/).

By participating, you agree to follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## Reporting a bug

If something does not work, for example the environment fails to install or the report does not render, please [open an issue](https://github.com/UBC-MDS-2026-27/DSCI-522-Group-34-Repository/issues) and include:

- what you were trying to do and the exact command you ran;
- the full error message;
- your operating system and the versions of R, uv and Quarto you are using (`R --version`, `uv --version`, `quarto --version`); and
- whether the problem happens after a fresh clone of the repository.

## Suggesting a change

For anything beyond a small fix, please open an issue describing the change before you start working on it. This lets the team discuss whether it fits the project and avoids duplicated effort. Small fixes, such as a spelling mistake in the report, can go straight to a pull request.

## Submitting your work

We use the [GitHub flow](https://docs.github.com/en/get-started/using-github/github-flow) workflow.

1. **Core team members** create a branch in this repository. **External contributors** fork the repository and create a branch in their fork.
2. Give the branch a short, descriptive name, such as `fix-figure-labels` or `add-eda-table`.
3. Keep each branch focused on one piece of work.
4. Set up both environments from the repository root: run `uv sync` for Python, and run `renv::restore()` in R for the R packages.
5. Make your changes, then render the report with `quarto render analysis/predicting-paid-math-classes.qmd` and check that it builds without errors.
6. Commit with clear messages that explain what changed and why, for example `Add stratified train/test split before EDA`.
7. Push your branch and open a pull request against `main`. Describe what you changed, link the related issue (for example, `Closes #12`), and point out anything reviewers should check closely.
8. At least one other team member must review and approve the pull request before it is merged. Nobody pushes directly to `main`.

If you add a package, record it so everyone gets the same environment:

- **Python:** add it with `uv add <package>`, and commit both `pyproject.toml` and `uv.lock`.
- **R:** install it with `renv::install("<package>")`, use it in the report, run `renv::snapshot()`, and commit `renv.lock`.

## Style

- R code should follow the [tidyverse style guide](https://style.tidyverse.org/).
- Python code should follow [PEP 8](https://peps.python.org/pep-0008/).
- Use descriptive variable names and comment any step that is not obvious.
- Write report text in full sentences, use plain-English feature names rather than code variable names, and spell out acronyms the first time you use them.
- Every figure and table in the report needs a number and a caption, and must be referred to in the text.

## AI policy

You may use generative AI tools, such as ChatGPT, Claude or GitHub Copilot, when contributing to this project, under the following conditions.

**What is allowed.** You may use AI tools to help you write or debug code, draft or edit text, explain error messages or concepts, and double-check code before a pull request is merged.

**What is not allowed.**

- Issues and pull requests must be opened by a person, not by an AI agent or bot. Pull request reviews and merge decisions are made by people.
- Do not submit code or text that you do not understand and cannot explain. If a reviewer asks why something works, "the AI wrote it" is not an acceptable answer.
- Do not use AI tools to generate references. Every citation must be checked against its original source, because AI tools can invent publications that do not exist.

**What you must disclose.** If you used AI tools for a substantial part of a contribution (more than small autocompletions), say so in the pull request description: name the tool and briefly describe what it helped with. If you used instruction files, such as a `CLAUDE.md` or a saved system prompt, commit them to the repository.

**Who is responsible.** The person who opens a pull request is fully responsible for its content, including its correctness, its licensing and any errors introduced by AI tools. Reviewers should apply the same standard to AI-assisted contributions as to any other contribution.

## Questions

If you are unsure about anything, open an issue and ask. We are happy to help.
