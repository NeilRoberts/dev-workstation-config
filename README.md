# macOS Dev Workstation Configuration

Notes on the applications and tools that I have installed on my Mac for
non-Xcode development. While I have tried to maintain a logical ordering,
some steps may appear earlier than their prerequisites. Follow at your own
risk.

## Standalone Tools and Frameworks

## Homebrew

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Homebrew [project](https://brew.sh)

### git

```bash
brew install git
```

### Maven

```bash
brew install maven
```

### pyenv and pyenv-virtualenv

```bash
brew install pyenv pyenv-virtualenv
```

pyenv [project](https://github.com/pyenv/pyenv)

pyenv-virtualenv [project](https://github.com/pyenv/pyenv-virtualenv)

## Programming Languages

### Python

```bash
pyenv install 2.7.15
pyenv install 3.6.6
pyenv install 3.7.0
```

#### Set the preferred order of Python versions:

```bash
pyenv global 3.6.6 3.7.0 2.7.15 system
```

pyenv global [docs](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md#pyenv-global-advanced)

#### Create and activate a virtualenv for Python 3.6

```bash
pyenv virtualenv 3.6.6 py3.6
pyenv activate py3.6
```

### Ruby

#### Ruby Version Manager (rvm)

```bash
curl -sSL https://get.rvm.io | bash -s stable
```

rvm [project](https://rvm.io)

#### Latest Ruby version

```bash
rvm install ruby --latest
```

#### Ruby documentation

```bash
rvm docs generate-ri
```
