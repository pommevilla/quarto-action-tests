# Quarto Action Testing

Testing for creating a Github action that renders a project via `quarto`. The action file is [quarto-render](.github/workflows/quarto-render.yml). Some requirements:

* A file named `requirements.txt`. You can generate this via `pip freeze > requirements.txt`.
* An `Renv` lockfile. See [here](https://rstudio.github.io/renv/articles/renv.html#workflow-1) for more information on using `Renv` and creating lockfiles/snapshots.

## Steps

The action will render the documents in the directory by taking these steps:

1. Downloading and installing the latest Quarto CLI release from [quarto-dev/quarto-cli](https://github.com/quarto-dev/quarto-cli)
2. Set up Python via [actions/setup-python](https://github.com/actions/setup-python)
3. Install all Python requirements from `requirements.txt` (parsing for platform specific packages)
4. Set up R via [r-lib/actions/setup-r](https://github.com/r-lib/actions/tree/master/setup-r)
5. Restore the R environment from the `renv` lockfile
6. Calls `quarto render` at the root of the github repository.
7. Pushes and commits any changes detected.
