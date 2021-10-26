# Redesigning Docs Websites

The documentation of my projects is Open Source and managed by [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).

All projects will have in future days their own GitHub repository documentation accessible at `https://llaville.github.io/<project>`

Documentation websites are hosted by [Github Pages](https://pages.github.com/)

## Step by step

1. Creates your own repository as explained on [Github Pages](https://pages.github.com/).

2. Creates template of your project documentation with [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).

3. Deploys built documentation to your GitHub Pages project repository.

### Step 1 - Your GitHub Pages

Head over to GitHub and create a new public repository named `<username>.github.io`,
where <username> is your username (or organization name) on GitHub.

### Step 2 - Configuration

Follows recommendation for [creating your site](https://squidfunk.github.io/mkdocs-material/creating-your-site/),
to make your `docs` folder and `mkdocs.yml` configuration file.

### Step 3 - Deploy

Build and deploy documentation using [GitHub Actions](https://squidfunk.github.io/mkdocs-material/publishing-your-site/#with-github-actions)

1. [Set up your GitHub Actions workflow with a specific version of python](https://github.com/actions/setup-python).
2. [Install Material for MkDocs](https://squidfunk.github.io/mkdocs-material/getting-started/#with-pip) with pip.
3. [Checkout Project Source Code](https://github.com/actions/checkout).

```yaml
jobs:
    deploy:
        name: Deploy docs
        runs-on: ubuntu-latest
        steps:
          -   # Setup Python version
            name: Setup Python
            uses: actions/setup-python@v2
            with:
              python-version: 3.x

          -   # Install Material for MkDocs
            name: Install Material for MkDocs
            run: pip install mkdocs-material

          -   # Git Checkout
            name: Checkout Code
            uses: actions/checkout@v2
            with:
              fetch-depth: 0

          -   # Build and deploy Documentation
            name: Build Docs
            run: mkdocs gh-deploy --force
```
