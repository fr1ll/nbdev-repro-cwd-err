nbdev-repro-cwd-err
================

<!-- WARNING: THIS FILE WAS AUTOGENERATED! DO NOT EDIT! -->

## Description of the error

The notebook `nbs/00_core.ipynb` reproduces an error with `nbdev_readme`
I’m trying to understand in my
[`clip-plot`](https://github.com/fr1ll/clip-plot) repo.

Intended behavior: Copy some data from a path relative to code execution
(the `assets` folder) into a code relative to the current working
directory:

``` python
from shutil import copytree
from pathlib import Path
src = Path(__file__).parents[1] / "assets"
dest = Path().cwd() / "output"
copytree(src, dest, dirs_exist_ok=True)
```

Since the `__file__` attribute doesn’t exist in the notebook, I first
set it to `Path().cwd()` in a cell with a `#| hide` directive.

Observations: - The notebook runs fine on its own - `nbdev_test`
passes - the script `00_core.py` created by `nbdev_export` runs fine -
`nbdev_readme` fails with this error due to `00_core.ipynb`:

``` python
NameError: name '__file__' is not defined
```

- If I set `__file__` to cwd *without* a `#| hide` directive, I get cwd
  as the root of my repo rather than as the `nbds` or other folder.

Basic question: It looks like `nbdev_readme` runs `00_core.ipynb` in
iPython. What’s the best way to execute stuff that we don’t want to run
in the script, such as setting `__file__`? What’s the best way to think
about this?

## Install

``` sh
pip install nbdev_repro_cwd_err
```
