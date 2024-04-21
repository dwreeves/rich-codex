## Config locations

Rich-codex can be run in several different ways and get configuration from multiple different locations.
They are, in order of parsing / precidence (last location wins):

<!-- prettier-ignore-start -->

- Global, for entire run:
    - GitHub Action arguments
    - Environment variables
    - Command-line flags (CLI)
    - Rich-codex config files (`.rich-codex.yml`)
- Per-image:
    - Rich-codex config files (`.rich-codex.yml`)
    - Markdown config

<!-- prettier-ignore-end -->

## Overview of all options

An overview of all available config options in all scopes is below:

| CLI                    | Environment variable | GitHub Action / Rich-codex config |
| ---------------------- | -------------------- | --------------------------------- |
| `--search-include`     | `SEARCH_INCLUDE`     | `search_include`                  |
| `--search-exclude`     | `SEARCH_EXCLUDE`     | `search_exclude`                  |
| `--no-search`          | `NO_SEARCH`          | `no_search`                       |
| `--command`            | `COMMAND`            | `command`                         |
| `--timeout`            | `TIMEOUT`            | `timeout`                         |
| `--working-dir`        | `WORKING_DIR`        | `working_dir`                     |
| `--before-command`     | `BEFORE_COMMAND`     | `before_command`                  |
| `--after-command`      | `AFTER_COMMAND`      | `after_command`                   |
| `--snippet`            | `SNIPPET`            | `snippet`                         |
| `--snippet-syntax`     | `SNIPPET_SYNTAX`     | `snippet_syntax`                  |
| `--img-paths`          | `IMG_PATHS`          | `img_paths`                       |
| `--clean-img-paths`    | `CLEAN_IMG_PATHS`    | `clean_img_paths`                 |
| `--configs`            | `RC_CONFIGS`         | `rc_configs`                      |
| `--fake-command`       | `FAKE_COMMAND`       | `fake_command`                    |
| `--hide-command`       | `HIDE_COMMAND`       | `hide_command`                    |
| `--title-command`      | `TITLE_COMMAND`      | `title_command`                   |
| `--head`               | `RC_HEAD`            | `head`                            |
| `--tail`               | `RC_TAIL`            | `tail`                            |
| `--trim-after`         | `TRIM_AFTER`         | `trim_after`                      |
| `--truncated-text`     | `TRUNCATED_TEXT`     | `truncated_text`                  |
| `--skip-git-checks`    | `SKIP_GIT_CHECKS`    | `skip_git_checks`                 |
| `--no-confirm`         | `NO_CONFIRM`         | -                                 |
| `--min-pct-diff`       | `MIN_PCT_DIFF`       | `min_pct_diff`                    |
| `--skip-change-regex`  | `SKIP_CHANGE_REGEX`  | `skip_change_regex`               |
| `--terminal-width`     | `TERMINAL_WIDTH`     | `terminal_width`                  |
| `--terminal-min-width` | `TERMINAL_MIN_WIDTH` | `terminal_min_width`              |
| `--notrim`             | `NOTRIM`             | `notrim`                          |
| `--terminal-theme`     | `TERMINAL_THEME`     | `terminal_theme`                  |
| `--snippet-theme`      | `SNIPPET_THEME`      | `snippet_theme`                   |
| `--use-pty`            | `USE_PTY`            | `use_pty`                         |
| `--created-files`      | `CREATED_FILES`      | -                                 |
| `--deleted-files`      | `DELETED_FILES`      | -                                 |
| `--verbose`            | `LOG_VERBOSE`        | `log_verbose` \*                  |
| `--save-log`           | `LOG_SAVE`           | -                                 |
| `--log-file`           | `LOG_FILENAME`       | -                                 |
| -                      | -                    | `commit_changes` \*               |
| -                      | -                    | `error_changes` \*                |
| -                      | -                    | `title` †                         |
| -                      | -                    | `extra_env` †                     |
| -                      | -                    | `skip` †                          |

- `*` - GitHub Action only
- `†` - Markdown / config only (per-output, not global)

## Description of options

A brief description of each option follows.

<!-- prettier-ignore-start -->
!!! note
    Hopefully all config options will be either fairly self-explanitory and/or documented in more details elsewhere.
    If not, please open an issue on GitHub
<!-- prettier-ignore-end -->

- `--search-include`: Glob patterns to search for rich-codex comments
- `--search-exclude`: Glob patterns to exclude from search for rich-codex comments
- `--no-search`: Set to disable searching for rich-codex comments
- `--command`: Specify a command to run to capture output
- `--timeout`: Maximum run time for command (seconds)
- `--hide-command`: Hide the terminal prompt with the command at the top of the output
- `--title-command`: Use the command as the terminal title if not set explicitly
- `--head`: Show only the first N lines of output
- `--tail`: Show only the last N lines of output
- `--trim-after`: Don't print any more lines after this string is found
- `--truncated-text`: Text to show when --head or --tail truncate content
- `--snippet`: Literal code snippet to render
- `--snippet-syntax`: Language to use for snippet sytax highlighting
- `--img-paths`: Path to image filenames if using 'command' or 'snippet'
- `--clean-img-paths`: Remove any matching files that are not generated
- `--configs`: Paths to YAML config files
- `--skip-git-checks`: Skip safety checks for git repos
- `--no-confirm`: Set to skip confirmation prompt before running commands
- `--min-pct-diff`: Minimum file percentage change required to update image
- `--skip-change-regex`: Skip image update if file changes match regex
- `--terminal-width`: Width of the terminal
- `--terminal-min-width`: Minimum width of the terminal when trimming
- `--notrim`: Disable automatic trimming of terminal width
- `--terminal-theme`: Colour theme
- `--snippet-theme`: Snippet Pygments theme
- `--use-pty`: Use a pseudo-terminal for commands (may capture coloured output)
- `--created-files`: Save a list of created files to this file
- `--deleted-files`: Save a list of deleted files to this file
- `--verbose`: Print verbose output to the console.
- `--save-log`: Save a verbose log to a file (automatic filename).
- `--log-file`: Save a verbose log to a file (specific filename).
- `commit_changes`: Automatically commit changes to the repository
- `error_changes`: Exit with an error if changes are found (Ignored if `commit_changes` is true)
- `title`: Title for the terminal title bar
- `skip`: Skip / ignore this image
