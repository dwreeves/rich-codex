---
title: GitHub Action
---

Rich-codex was primarily designed to run automatically with GitHub actions, to keep your screenshots up to date for you.

If there are changes to the images, the action can exit with an error (default) or automatically commit the updates.

A very simple example is shown below. This action looks for rich-codex content in the repo, generates the images and then creates and pushes a new commit with any changes.

```yaml
on: [push]
jobs:
  rich_codex:
    runs-on: ubuntu-latest
    steps:
      - name: Check out the repo
        uses: actions/checkout@v3

      - name: Install your custom tools
        run: pip install .

      - name: Generate terminal images with rich-codex
        uses: ewels/rich-codex@v1
        with:
          commit_changes: "true"
```

For a more complex example, see [`.github/workflows/examples.yml`](.github/workflows/examples.yml) in this repository.

<!-- prettier-ignore-start -->
!!! info
    For GitHub Actions to push commits to your repository, you'll need to set _Workflow permissions_ to _Read and write permissions_ under _Actions_ -> _General_ in the repo settings. See the [GitHub docs](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/enabling-features-for-your-repository/managing-github-actions-settings-for-a-repository#configuring-the-default-github_token-permissions).
<!-- prettier-ignore-end -->

## GitHub Action Inputs

- `search_include`: Glob patterns to files in which to search for rich-codex comments
- `search_exclude`: Glob patterns to exclude from search for rich-codex comments
- `no_search`: Set to 'true' to disable searching for rich-codex comments
- `command`: Specify a command to run to capture output
- `snippet`: Literal code snippet to render
- `snippet_syntax`: Language to use for snippet sytax highlighting
- `img_paths`: Path to image filenames if using 'command' or 'snippet'
- `clean_img_paths`: Remove any matching files that are not generated
- `rc_configs`: Paths to YAML config files
- `min_pct_diff`: Minimum file percentage change required to update image
- `skip_change_regex`: Skip image update if file changes match regex
- `width`: Width of the terminal
- `theme`: Colour theme
- `use_pty`: Use a pseudo-terminal for commands (may capture coloured output)
- `log_verbose`: Print verbose output to the console.
- `commit_changes`: Automatically commit changes to the repository
- `error_changes`: Exit with an error if changes are found (Ignored if 'commit_changes' is true)