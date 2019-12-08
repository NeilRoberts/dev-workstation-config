# macOS Dev Workstation Configuration

These are my notes on the applications and tools that I installed on my Mac for
(primarily) non-Xcode development. For the most part, these steps are in
chronological order, but YMMV. I've updated this document for my latest macOS
Catalina (10.15.1) setup.

## Xcode Command Line Tools

Install the Xcode Command Line Tools. When prompted, choose Install and Agree to the license agreement.

```bash
xcode-select --install
```

## iTerm 2

Download [iTerm](https://iterm2.com/downloads.html) and extract it to `/Applications`

### Dracula Theme for iTerm

Clone the Dracula repository and follow the [instructions](https://draculatheme.com/iterm/) to activate the theme in iTerm 2

```bash
mkdir ~/src
cd ~/src
git clone https://github.com/dracula/iterm.git
```

## Oh My Zsh

Install Oh My Zsh. When prompted, enter your user password.

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

oh-my-zsh [project](https://github.com/robbyrussell/oh-my-zsh_)

## Homebrew

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Homebrew [project](https://brew.sh)

## git

```bash
brew install git

# Global git ignore
echo ".DS_Store" >> ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global

# User info
git config --global user.name "Firstname Lastname"
git config --global user.email your_email@host.tld
```

## Docker

Download the latest [stable release](https://docs.docker.com/docker-for-mac/release-notes/) of Docker CE for Mac and copy it to `/Applications`. Launch Docker.app to complete installation.

## Visual Studio Code

Download [VS Code](https://code.visualstudio.com/Download) and extract it to `/Applications`

Useful extensions:

* Docker (ms-azuretools.vscode-docker)
* Dracula Official theme (dracula-theme.theme-dracula)
* Git History (donjayamanne.githistory)
* GitLens (eamodio.gitlens)
* Go (ms-vscode.go)
* markdownlint (davidanson.vscode-markdownlint)
* Python (ms-python.python)

Follow the [instructions](https://draculatheme.com/visual-studio-code/) to activate the theme in VS Code

## Python

```bash
# Install pyenv and pyenv-virtualenv
brew install pyenv pyenv-virtualenv

# Configure pyenv and pyenv-virtualenv
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
source ~/.zshrc

# List the available Python versions
pyenv install --list

# Install the latest Python 3
pyenv install 3.8.0

# Set the preferred order of Python interpreters
pyenv global 3.8.0 system

# Create and activate a Python virtual environment
pyenv virtualenv 3.8.0 sandbox-3.8.0
pyenv activate sandbox-3.8.0
```

pyenv [project](https://github.com/pyenv/pyenv)

pyenv-virtualenv [project](https://github.com/pyenv/pyenv-virtualenv)

pyenv global [docs](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md#pyenv-global-advanced)

## Ruby

```bash
# Install rvm
curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm

# List the available Ruby versions
rvm list known

# Install the latest Ruby
rvm install ruby --latest

# Install the Ruby documentation
rvm docs generate-ri
```

rvm [project](https://rvm.io)

## Go

```bash
brew install go
```

## Java

### Maven

```bash
brew install maven
```
