# Editable install w/ pylint

Demonstrates that an editable install with py-build-cmake is different from a setuptools install in a way that breaks pylint.
Tested with pylint 2.14.3 on macOS.

In both sub-projects, the following commands:

First, install prerequisites:

```sh
python3 -m venv venv
. venv/bin/activate
pip install -U pip
pip install pylint
```

Now test pylint with a normal install:

```sh
pip install .
python test.py
pylint test.py
pip uninstall -y foo
```

You should see that `test.py` runs successfully and pylint works correctly on the file for both setuptools and py-build-cmake.

Now test pylint with an editable install:

```sh
pip install -e .
python test.py
pylint test.py
pip uninstall -y foo
```

You should see that `test.py` runs successfully.
However, pylint works correctly on the file for the setuptools version, but the py-build-cmake version results in both `import-error` and `no-name-in-module` errors.
