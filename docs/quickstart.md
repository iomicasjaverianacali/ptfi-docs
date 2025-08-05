# How get access to project's documentation

Be sure that you have python installed. Open a terminal and:

1. Install the required repositories

```sh
pip install mkdocs-material
```

```sh
pip install 'mkdocstrings[python]'
```

```sh
pip install mkdocs-glightbox
```

2. Set the current directory to the directory containing the file `mkdocs.yml`

3. Execute

```sh
mkdocs serve
```

4. Open the hyperlink (localhost:80000 or 127.0.0.1:8000) by clicking it or by copying and pasting it in the web browser.