# Redesigning Docs Websites

The documentation of my projects is Open Source and managed by [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/).

All projects will have in future days their own GitHub repository documentation accessible at `https://llaville.github.io/<project_name>`

Documentation websites are hosted by [Github Pages](https://pages.github.com/)

After many search, and read article [Custom GH Pages deploys made easy](https://dev.to/michaelcurrin/github-pages-deploys-made-easy-343o),
I've adopted the [peaceiris/actions-gh-pages](https://github.com/peaceiris/actions-gh-pages) GitHub Action.

## Similar articles

- [Publish your Markdown docs on GitHub Pages](https://dev.to/ar2pi/publish-your-markdown-docs-on-github-pages-6pe)
- [MkDocs : Static HTML sites and documentation preparation tool that you can host on GitHub pages](https://dev.to/sandeepbalachandran/mkdocs-static-html-sites-and-documentation-preparation-tool-that-you-can-host-on-github-pages-262f)

## My Workflow

### Build steps

- The first part of the workflow (<1>, <2>, <3>) set up environment to builds the site.
- The second part of the workflow (<4>) builds the site contents.
- The last part of the workflow (<5>) deploy the site on `gh-pages` branch of the repository.

<1> [Checkout Project Source Code](https://github.com/actions/checkout).
```yaml
     -   # Git Checkout
        name: Checkout Code
        uses: actions/checkout@v2
        with:
          persist-credentials: false
```

<2> [Set up your GitHub Actions workflow with a specific version of python](https://github.com/actions/setup-python).
```yaml
      -   # Setup Python version
        name: Set up Python runtime
        uses: actions/setup-python@v2
        with:
          python-version: 3.x
```

<3> [Install Material for MkDocs](https://squidfunk.github.io/mkdocs-material/getting-started/#with-pip) with pip.
```yaml
     -   # Install Material for MkDocs
       name: Install Material for MkDocs
       run: pip install mkdocs-material
```

<4> Build documentation with [MkDocs](https://www.mkdocs.org/) one of the most famous [static site generators](https://jamstack.org/generators/)
```yaml
      -   # Build Documentation
        name: Build Docs
        run: mkdocs build
```

<5> Deploy documentation to [Github Pages](https://pages.github.com/)
```yaml
      -   # Deploy Documentation
        name: Deploy Docs
        if: ${{ github.ref == 'refs/heads/master' }}
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./site
```
