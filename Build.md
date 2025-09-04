# Build

## Build package

```bash
uv build
```

## Build docs

```bash
VERSION=$(uv run python -c "from importlib.metadata import version; import fffio; print(version('fffio'))")
uv run sphinx-apidoc -F -H fffio -V v$VERSION -o docs src
```

Change docs/conf.py:

```diff
  extensions = [
      'sphinx.ext.autodoc',
      'sphinx.ext.viewcode',
      'sphinx.ext.todo',
+     'sphinx_rtd_theme',
+     'sphinx.ext.napoleon',
  ]

- html_theme = 'alabaster'
- html_static_path = ['_static']
+ html_theme = 'sphinx_rtd_theme'
```

Change docs/fffio.rst like this if you want to avoid Sphinx's warning:

```diff
- Submodules
- ----------

  .. automodule:: fffio.frame_reader
+    :noindex:

  .. automodule:: fffio.frame_writer
+    :noindex:

- Module contents
- ---------------
- 
- .. automodule:: fffio
-    :members:
-    :show-inheritance:
-    :undoc-members:
```

```bash
uv run sphinx-build docs docs/_build
```
