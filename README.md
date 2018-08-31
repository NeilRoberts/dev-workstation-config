# dev-workstation-config

Notes on my workstation config - may not be safe for public consumption

## Standalone Tools and Frameworks

### Homebrew

Project [site](https://brew.sh)

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## Programming Languages

### Python

#### pyenv

See the [installation instructions](https://github.com/pyenv/pyenv)

```bash
brew update
brew install pyenv
```

#### pyenv-virtualenv

See the [installation instructions](https://github.com/pyenv/pyenv-virtualenv)

```bash
brew install pyenv-virtualenv
```

#### Python versions

```bash
pyenv install 2.7.15
pyenv install 3.6.6
pyenv install 3.7.0
```

Set the preferred order of Python versions:

```bash
pyenv global 3.6.6 3.7.0 2.7.15 system
```

pyenv global [docs](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md#pyenv-global-advanced)

#### Create and activate a virtualenv for Python 3.6

```bash
pyenv virtualenv 3.6.6 py3.6
pyenv activate py3.6
```
