# rich-codex ⚡️📖⚡️

A [command-line tool](#command-line) and [GitHub Action](#github-action) to generate screengrab images of a terminal window containing code snippets or outputs from commands.

It can be configured in four different ways:

- [Markdown images](#markdown-images): Search markdown files for images with `commands` as their alt texts.
- [Markdown comments](#markdown-comments): Search markdown files for special HTML comments.
- [Command-line / action inputs](#command-line-action-inputs): Specify a command or snippet using the action `with` inputs.
- [Config files](#yaml-config-files): Use one or more YAML config files for multiple images and more complex customisation.

Images can be generated as SVG, PNG or PDF (detected by filename extension).

## Usage

### Command-line

At its simplest, the command-line tool runs without any arguments and recursively searches the current working directory for anything it recognises:

```bash
pip install rich-codex
rich-codex
```

Behaviour can be customised on the command-line with environment variables, see `rich-codex --help`:
![`rich-codex --help`](docs/img/rich-codex-help.svg)

If generating PNG or PDF, you'll need [CairoSVG](https://cairosvg.org/documentation/) installed.
You may prefer to use the `ewels/richcodex` docker container which contains everything you need.

Usage is typically as follows:

```bash
docker run v `pwd`:`pwd` -w `pwd` -u $(id -u):$(id -g) ewels/richcodex
```

- The `-v` argument tells Docker to bind your current working directory (`pwd`) to the same path inside the container, so that files created there will be saved to your local file system outside of the container.
- `-w` sets the working directory in the container to this path, so that it's the same as your working directory outside of the container.
- `-u` sets your local user account as the user inside the container, so that any files created have the correct ownership permissions.

You can then pass environment variables with the `-e` flag to customise behaviour.

### GitHub Action

This tool is designed to run automatically via a GitHub action, to keep your screenshots up to date for you.
Once the action generates images, it's up to you to use them however you like.

A very simple example is shown below.
This action looks for rich-codex content in the repo, generates the images and then creates and pushes a new commit with the changes.

```yaml
on: [push]
jobs:
  rich_codex:
    - name: Check out the repo
      uses: actions/checkout@v3

    - name: Install the tool and dependencies
      run: pip install .

    - name: Generate code images
      uses: ewels/rich-codex@v1

    - name: Add and commit new images
      uses: EndBug/add-and-commit@v9
      with:
        message: Generate new screengrabs with rich-codex
        committer_name: GitHub Actions
        committer_email: actions@github.com
```

## Generating images

### Markdown images

If you write markdown with images that contain _just_ a `backtick command` as the alt-text, rich-codex will find them.

For example, the following markdown will generate `docs/img/rich-codex-help.svg` (the image shown above) based on the output of the command `rich-codex --help`:

```markdown
This is getting meta!
![`rich-codex --help`](docs/img/rich-codex-help.svg)
```

> Note that this particular output is generated by the [rich-click](https://github.com/ewels/rich-click) package.
> This supports environment variables for setting terminal width and forcing terminal codes, so I set `TERMINAL_WIDTH=70` and `FORCE_COLOR=1`

### Markdown comments

```yaml
rich_codex:
  - uses: actions/checkout@v3
  - uses: ewels/rich-codex@v1
```

### Command-line / action inputs

### YAML config files

## How it works

Rich-codex uses the Python library [rich](https://github.com/textualize/rich) and also the command line tool [rich-cli](https://github.com/textualize/rich-cli/) under the hood.
These do all of the heavy lifting of actually creating the images.

Rich-codex is a simple wrapper that loads commands/snippets from various places, collects command outputs and then passes this to rich.
This command-line tool should really only be used in the context of the GitHub action, to auto-generate images from inline configs.
The [rich-cli](https://github.com/textualize/rich-cli/) tool is better for basically all other uses.

## Inputs

### `include`

Files to search for rich-codex comments.

### `exclude`

Files to exclude from search for rich-codex comments.

### `cmd`

Command to run.

### `snippet`

Literal code snippet to render.

### `img_paths`

Path to image filenames if using 'cmd' or 'snippet'.

### `configs`

Paths to YAML config files.

### `width`

Width of the terminal.

### `theme`

Colour theme.

## Outputs

### `images`

JSON array of all generated images.

### `svgs`

JSON array of all generated SVG files.

### `pngs`

JSON array of all generated PNG files.

### `pdfs`

JSON array of all generated PDF files.
