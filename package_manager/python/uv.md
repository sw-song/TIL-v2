reference: [Python UV: The Ultimate Guide to the Fastest Python Package Manager](https://www.datacamp.com/tutorial/python-uv)

Install uv via Homebrew
```
$ brew install uv
```

Check the uv version which is installed
```
$ uv --version
```

Initialize a new python project. This will initialize even git, gitignore and README files which are nessesary for building code project.
```
$ uv init your_project_folder_name
```

You can show up all of files with this command. If you have not installed 'tree' then you can do that with homebrew(`brew install tree`)
```
$ tree -a
```

There are .python-version file and pyproject.toml file. And with these two files, you can see how UV controll python version and packages that are installed in that project.
```
$ cat .python-version
```
```
> 3.9
```

```
$ cat pyproject.toml
```
```
> [project]
name = "test-v"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
requires-python = ">=3.9"
dependencies = []
```

If you install python packages, those will be added to dependencies in the `pyproject.toml`.
```
$ uv add matplotlib seaborn pandas numpy scikit-learn
```
uv know which python interpreter should be used and using this, It can make virtual environment at ./.venv
```
> Using CPython 3.9.6 interpreter at: /Library/Developer/CommandLineTools/usr/bin/python3
Creating virtual environment at: .venv
...
Successfully added all the requested packages! Here's what was installed:
Main packages you requested:
•  matplotlib==3.9.4
•  seaborn==0.13.2
•  pandas==2.3.0
•  numpy==2.0.2
•  scikit-learn==1.6.1
Dependencies that were also installed:
•  contourpy, cycler, fonttools, importlib-resources, joblib, kiwisolver, packaging, pillow, pyparsing, python-dateutil, pytz, scipy, six, threadpoolctl, tzdata, zipp

uv created a virtual environment at .venv using Python 3.9.6 and resolved all 30 packages in the dependency tree. All packages are now ready to use in your project!
```

And then, in pyproject.toml, you can see those packages are installed
```
$ cat pyproject.toml
```
```
[project]
name = "test-v"
version = "0.1.0"
description = "Add your description here"
readme = "README.md"
requires-python = ">=3.9"
dependencies = [
    "matplotlib>=3.9.4",
    "numpy>=2.0.2",
    "pandas>=2.3.0",
    "scikit-learn>=1.6.1",
    "seaborn>=0.13.2",
]
```

More importantly, uv add can resolve all dependencies so you don't need to care any verson conflict in normal cases.
and if you want, you can also see all packages which are installed in your virtual environment in uv.lock file.
The document says:
"UV automatically generates and updates a uv.lock file. This lock file serves several critical purposes like,
- It records the exact versions of all dependencies and their sub-dependencies that were installed.
- It ensures reproducible builds by "locking" dependency versions across different environments.
- It helps prevent "dependency hell" by maintaining consistent package versions.
- It speeds up installations since UV can use the locked versions instead of resolving dependencies again.


uv even support to run python file like this.
```
$ uv run hello.py
```

this means uv ensures that the script is executed inside the virtual environment in working project with `uv run`


If you want to use requirements.txt file to init your packages but also want to use uv, you can do like this,
```
$ pip freeze > requirements.txt
$ uv pip install -r requirements.txt
```
The opposite is also possible.
```
$ uv export -o requirements.txt
$ pip install -r requirements.txt
```

