# Contributing to Predicting Extra Paid Mathematics Classes

Thank you for your interest in this project. We welcome bug reports, suggestions, corrections to the report and improvements to the code. This guide explains how to contribute. It is adapted from the contributing guides of [dplyr](https://github.com/tidyverse/dplyr/blob/main/.github/CONTRIBUTING.md) and [Altair](https://github.com/vega/altair/blob/main/CONTRIBUTING.md). The AI policy below is adapted from the [SymPy AI-generated code policy](https://docs.sympy.org/dev/contributing/ai-generated-code-policy.html) and the [earthaccess AI policy](https://earthaccess.readthedocs.io/en/latest/contributor/ai-policy/).

By participating, you agree to follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## Reporting a bug

If something does not work, for example the container does not start or the report does not render, please [open an issue](https://github.com/UBC-MDS-2026-27/DSCI-522-Group-34-Repository/issues) and include:

- what you were trying to do and the exact command you ran;
- the full error message; if it's a container problem also provide the output of `docker compose logs`;
- your operating system and the Docker version you are using (`docker --version`); and
- whether the problem happens after a fresh clone of the repository.

## Suggesting a change

For anything beyond a small fix, please open an issue describing the change before you start working on it. This lets the team discuss whether it fits the project and avoids duplicated effort. Small fixes, such as a spelling mistake in the report, can go straight to a pull request. Edit the Quarto source `analysis/predicting-paid-math-classes.qmd`, not the rendered HTML.

## Setting up the project

We develop in the same Docker container that users run the analysis in, so everyone uses the same versions of Python, R, Quarto, and every package. You do not install any packages on your own computer.

First follow the setup steps in the [README](README.md): install Docker, clone the repository, make an ssh key and download the image with `docker compose pull`. Run all the commands below from the root of the repository. 

## Working in the container with Positron

We edit and run the code inside the container, by connecting Positron to it over ssh.
Your project folder is shared with the container at `/workspace`,
so a file you change there changes on your computer too.

<details>
<summary><strong>Once, before your first connection</strong></summary>

1. Install [Positron](https://positron.posit.co/download.html) on your computer.
   Its **Remote SSH** feature, which connects to the container, comes built in,
   so you don't need to install an extension.
2. Make sure you followed the [Usage section of the README](README.md#usage):
   you have an ssh key at `~/.ssh/id_ed25519.pub` and you ran `docker compose pull`.
3. Check that Git knows who you are on your computer:

   ``` bash
   git config --global user.email
   ```

   It should print the email of your GitHub account.
   If it prints nothing, set your name and email:

   ``` bash
   git config --global user.name "Your Name"
   git config --global user.email "you@example.com"
   ```

   `docker-compose.yml` shares your `~/.gitconfig` with the container,
   so the commits you make there count as yours.

</details>

<details>
<summary><strong>Each time you work on the project</strong></summary>

1. In a terminal, in the root of this repository, start the container in the background:

   ``` bash
   docker compose up -d
   ```

   `docker compose ps` should list `analysis-env` as running.
2. In Positron, open the Command Palette
   (`Cmd+Shift+P` on Mac, `Ctrl+Shift+P` on Windows).
3. Type and run **Remote SSH: Show Remote Menu**, then pick **Connect to Host**.
4. Type `root@localhost:2222` and press Enter. A new Positron window opens.
   * If it asks for the platform of the remote host, pick **Linux**.
   * If it asks whether you trust the host (a "fingerprint"), click **Continue**.
   * The first time, Positron installs its server inside the container. This takes a few minutes (e.g., this takes > 5 minutes on Sky's computer).
5. **Open the project folder.**
   The bottom left corner now shows `SSH: localhost:2222`,
   but the Explorer says **No folder opened** and the terminal starts in `/root`,
   which has no project files. That is normal.
   * Click **Open Folder** in the Explorer.
   * Delete what is in the path box at the top of the window, type `/workspace`, and click "ok" (you may need to click "ok" a few times before this works).
   * The window reloads, and the Explorer shows **WORKSPACE [SSH: LOCALHOST:2222]** with the project files.
6. **Pick the Python interpreter** (check this every time).
   * Click the interpreter button at the top right of the window.
     The **Running Interpreter Sessions** menu only lists sessions that are already running
     (such as `/usr/bin/python3`, the container's system Python: not this one).
   * Click **New Console Session...** and pick
     **Python 3.14 (uv: dsci522-group34)**,
     with the path `/opt/venv/bin/python`. This is the environment built from `uv.lock`.
   * If it isn't in the list, run **Python: Select Interpreter** from the Command Palette,
     choose **Enter interpreter path...** and type `/opt/venv/bin/python`.
   * Don't pick `/workspace/.venv`: that is an environment from your own computer,
     and it doesn't run in the container.
   * To check, run `import sys; print(sys.executable)` in the Console.
     It should print `/opt/venv/bin/python`.
7. Work as usual. The Terminal, the Console and the **Render** button all run inside the container.
8. When you are done, close the Positron window,
   then stop and remove the container in a terminal on your computer:

   ``` bash
   docker compose down
   ```

</details>

<details>
<summary><strong>If it doesn't connect</strong></summary>

* **`~/.ssh/id_ed25519.pub` is a folder:** Docker made it because the key didn't exist yet.
  Run `docker compose down`, delete that folder, make the key
  (see the [README](README.md#usage)), and start again.
* **`~/.gitconfig` is a folder, or Git in the container doesn't know your name:**
  the same thing happened with your Git settings.
  Run `docker compose down`, delete that folder, set your name and email (see above), and start again.
* **It asks for a password:** the container can't see your key.
  Check that your key is named `id_ed25519.pub`, or change the key path in `docker-compose.yml`.
* **"Remote host identification has changed":** you are using a new image.
  Run `ssh-keygen -R "[localhost]:2222"`, then connect again.
* **GitHub asks you to sign in when you push from the container:**
  sign in once in the browser window Positron opens. Positron remembers it.
* **Linux laptops:** ssh refuses the key because the file belongs to you, not `root`.
  Remove the `#` from the `StrictModes no` line in the `Dockerfile` and push,
  so the workflow publishes a fixed image.
* **Port 2222 is already in use:** change the first `2222` in `docker-compose.yml`
  to another number (e.g. `2223`), and connect to that port instead.

More detail: [Working in a container over ssh with Positron](https://ubc-dsci.github.io/reproducible-and-trustworthy-workflows-for-data-science/lectures/containers-ssh-positron.html).

</details>

To re-run the analysis and render the report without opening the container:

``` bash
docker compose run --rm analysis-env uv run quarto render analysis/predicting-paid-math-classes.qmd
```


## Submitting your work

We use the [GitHub flow](https://docs.github.com/en/get-started/using-github/github-flow) workflow.

1. **Core team members** create a branch in this repository. **External contributors** fork the repository and create a branch in their fork.
2. Give the branch a short, descriptive name, such as `fix-figure-labels` or `add-eda-table`.
3. Keep each branch focused on one piece of work.
4. Make your changes in the container, then render the report (see the command above) and check that it builds without errors.
5. Commit with clear messages that explain what changed and why, for example `Add stratified train/test split before EDA`.
6. Push your branch and open a pull request against `main`. Describe what you changed, link the related issue (for example, `Closes #12`), and point out anything reviewers should check closely.
7. At least one other team member must review and approve the pull request before it is merged. Nobody pushes directly to `main`.

## Adding or updating a package
On a new branch, inside the container:

- **Python:** run `uv add <package>==<version>`, and commit both `pyproject.toml` and `uv.lock`.
- **R:** install it with `renv::install("<package>")`, use it in the report, run `renv::snapshot()`, and commit `renv.lock`.

Push the branch. Github Actions builds and publishes a new image, then commits the new `sha-` tag to `docker-compose.yml` on your branch. When the workflow finishes, run:
``` bash
git pull
docker compose pull
```

Then merge the branch into `main` in a pull request. After the merge builds the image again, everyone runs `git pull` on `main` and `docker compose pull`.

## Publishing the report

The report on Github Pages is a copy of the rendered report in `docs/index.html`.
Each time you re-render the report, copy it there, then commit and push:

``` bash
cp analysis/predicting-paid-math-classes.html docs/index.html
```

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
