Built with Material for Mkdocs:
https://squidfunk.github.io/mkdocs-material/

This website uses [mike](https://github.com/jimporter/mike) for versioning. To deploy a new release:
```
mike deploy --push --update-aliases MAJOR.MINOR.PATCH latest
```

There is a separate mkdocs-pdf.yml file to build a pdf version of this documentation.

# On Windows (PowerShell)
```
$env:ENABLE_PDF_EXPORT=1
mkdocs build -f mkdocs-pdf.yml
```