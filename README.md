# macOS Dev Workstation Configuration

Notes on the applications and tools that I have installed on my Mac for
non-Xcode development. While I have tried to maintain a logical ordering,
some steps may appear earlier than their prerequisites. Follow at your own
risk.

## Standalone Tools and Frameworks

## iTerm 2

Download [iTerm](https://iterm2.com/downloads.html) and extract it to `/Applications`

## Xcode Command Line Tools

Install the Xcode Command Line Tools. When prompted, choose Install and Agree to the license agreement.

```bash
xcode-select --install
```

In macOS 10.14 Mojave, headers are no longer installed into `/usr/include` by default. For programs that haven't been updated, Apple has provided a package to install the headers. **Don't install them unless a problem occurs later.** When prompted, enter your administrator password.

```bash
sudo installer -pkg /Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg -target /
```

## git config

```bash
# Global git ignore
echo ".DS_Store" >> ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global

# User info
git config --global user.name "Firstname Lastname"
git config --global user.email your_email@host.tld
```

### Oh My Zsh

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

### Dracula Theme for iTerm

Clone the Dracula repository and follow the [instructions](https://draculatheme.com/iterm/) to activate the theme in iTerm 2

```bash
mkdir ~/src
cd ~/src
git clone https://github.com/dracula/iterm.git
```

### pyenv and pyenv-virtualenv config

```bash
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
source ~/.zshrc
```

## Docker

Download the latest [stable release](https://docs.docker.com/docker-for-mac/release-notes/) of Docker CE for Mac and copy it to `/Applications`. Launch Docker.app to complete installation.

## Visual Studio Code

Download [VS Code](https://code.visualstudio.com/Download) and extract it to `/Applications`

Useful extensions:

* Python (ms-python.python)
* Dracula Official theme (dracula-theme.theme-dracula)
* GitLens (eamodio.gitlens)
* Git History (donjayamanne.githistory)
* Docker (peterjausovec.vscode-docker)
* markdownlint (davidanson.vscode-markdownlint)

## Programming Languages

### Python

```bash
pyenv install 3.7.3
pyenv install 3.6.8
pyenv install 2.7.16
```

#### Set the preferred order of Python versions:

```bash
pyenv global 3.7.3 3.6.8 2.7.16 system
```

pyenv global [docs](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md#pyenv-global-advanced)

#### Create and activate a virtualenv for Python 3.7

```bash
pyenv virtualenv 3.7.3 sandbox-3.7.3
pyenv activate sandbox-3.7.3
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
