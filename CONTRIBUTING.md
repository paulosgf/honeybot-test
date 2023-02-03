## 📃 Quickstart

fork repo, run run.py in /honeybot/run.py

## 📃 Full Contributing Guide

- Don't forget to add your country flag on the README.md after accepted PR. I'll have to hunt it down on your profile if you don't.
- Make sure to follow PEP8

### Code Style

#### Black formatting

The codebase is formatted using [black](https://github.com/psf/black) with a custom set of rules found in [pyproject.toml](./pyproject.toml).

Run command: `black --config ./pyproject.toml src/honeybot/`

#### Isort formatting

The various imports must be sorted alphabetically using [isort](https://github.com/PyCQA/isort). Custom rules found in [pyproject.toml](./pyproject.toml).

Run command: `isort --check-only --settings-path ./pyproject.toml src/honeybot/`

#### Bandit security checks

[Bandit](https://github.com/PyCQA/bandit) is used to screen for security issues in the code. Custom rules found in [pyproject.toml](./pyproject.toml).

Run command: `bandit -ll -c ./pyproject.toml -r .`

#### Sanity checks

Sanity checks must pass to ensure that honeybot functionality is not broken as new code is merged.

Run command: `python src/honeybot/test_core.py`

### Pull Request

First clone the project

```
git clone https://github.com/pyhoneybot/honeybot.git
```

cd into the project

```
cd honeybot
```

create a virtualenv to work with different python libs versions

```
python -m venv venv
source venv/bin/activate
```

install the tools needed to make the constraint checks

```
pip install black isort bandit pre-commit
pre-commit install
```

different changes to different files. For example, for someone making a weather plugin, first he creates a new branch

```
git checkout -b "weather-plugin"
```

then he commits

```
git add *
git commit -m "added weather plugin"


or


git commit -a -m "did this"
```

then he push to create a PR with the branch

```
git push origin head


or


git push origin weather-plugin
```

Now let us say he wants to work on another issue, such as adding a joke in the jokes plugin. He creates another branch

```
git checkout -b "add-jokes"
```

then, after writing the code, follow the same steps as before

```
git add *
git commit -m "added some jokes"
git push origin head
```

Now he wants to go back to fixing his weather plugin, he changes branch

```
git checkout weather-plugin
```

test if all files are well formatted, complying with style and security rules, before send the PR

```
black --check --verbose --config ./pyproject.toml src/honeybot/plugins/downloaded/weather/main.py
isort --check-only --settings-path ./pyproject.toml src/honeybot/plugins/downloaded/weather/main.py
bandit -ll -c ./pyproject.toml -r src/honeybot/plugins/downloaded/weather/main.py 
```

then commit

```
git add *
git commit -m "fixed <issue>"
```

then a PR

```
git push origin head
```

### Why all these?

So as not to reject a whole PR just because of some oddities. Reject only unneeded part.

### Updating the Documentation

If you created a new plugin you should add your plugin to the documentation.
To do this, go into your cloned honeybot repo and then into the directory _docs/source/Plugins_ .
Depending on the type of plugin write this into the development, fun, miscellaneous or utility RST file:

```rst

   <Plugin-Name>
   ^^^^^^^^^^^^^
   .. automodule:: plugins.<your-plugin-filename>
      :members:
```

This allows sphinx to automatically pull the docstrings from the code of your plugin and parse them accordingly.

Further reading: [Honeybot Docs](https://pyhoneybot.github.io/honeybot/How_Tos/documentation.html), [First Contributions](https://github.com/firstcontributions/first-contributions)

## 🥄 Updating fork

Now, other changes are ongoing, what if you need the latest changes?

```
git pull origin master
```

helps if you cloned your own repo. What if you want to update your local copy of someone else's repo that you forked?
You do it like that

```
cd <your/local/cloned/repo/path/here>
git remote add upstream https://github.com/pyhoneybot/honeybot.git
git fetch upstream
git pull upstream master
```
