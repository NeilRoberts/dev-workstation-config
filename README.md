# macOS Dev Workstation Configuration

## Overview

This documents the applications and tools that I've installed on my Macs for software development. The steps are mostly in order, but YMMV. These instructions should work on both macOS Catalina 10.15.x and macOS Big Sur 11.x, but I've only checked them recently on Big Sur.

## Big Sur notes

### System Settings

- Enable tap to click
- Increase tracking speed
- Increase cursor size by one step
- Enable three-finger drag

### macOS Big Sur 11.1 Base Install Tool Versions

| Tool     | Command               | Version  | Notes                                                           |
| -------- | --------------------- | -------- | --------------------------------------------------------------- |
| Git      | `git`                 | N/A      | Exists in `/usr/bin` but requires Xcode CLT                     |
| Perl     | `perl`                | 5.28.2   | 5.18.4 (`perl5.18`) and 5.30..2 (`perl5.30`) are also installed |
| PHP      | `php`                 | 7.3.24   | "Not recommended" - will be removed in future macOS             |
| Python 2 | `python` or `python2` | 2.7.16   |                                                                 |
| Python 3 | `python3`             | N/A      | Exists in `/usr/bin` but requires Xcode CLT                     |
| Ruby     | `ruby`                | 2.6.3p62 |                                                                 |

## Xcode Command Line Tools - if Xcode is unnecessary or inaccessible

Install the Xcode Command Line Tools. When prompted, choose Install and Agree to the license agreement.

```sh
xcode-select --install
```

## Xcode

Install Xcode from the Mac App Store. Launch, agree to the license agreement and enter password when prompted.

## iTerm 2

Download [iTerm](https://iterm2.com/downloads.html) and extract it to `/Applications`. Enable
unlimited scrollback: `Profiles > Terminal > Unlimited scrollback`

### Dracula Theme for iTerm

Clone the Dracula repository and follow the [instructions](https://draculatheme.com/iterm/) to activate the theme in iTerm 2

```sh
mkdir ~/src
cd ~/src
git clone https://github.com/dracula/iterm.git dracula_iterm
```

## Oh My Zsh

```sh
# Install Oh My Zsh and enter user password when prompted
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Enable zsh-autosuggestions
cd ~/.oh-my-zsh/custom/plugins
git clone https://github.com/zsh-users/zsh-autosuggestions

nano ~/.zshrc
# Scroll down to the plugins section and add zsh-autosuggestions to the space-separated list
# Save, exit, and open a new terminal window for changes to take effect
```

oh-my-zsh [project](https://github.com/robbyrussell/oh-my-zsh_)

## SSH Key Pair

```sh
# For GitHub. Other repos may require a different algorithm
ssh-keygen -t ed25519 -C "your_email_address@host.tld"

# Press "Enter" to accept the default file location

# Enter a passphrase for the new key pair
```

GitHub has [more info][github-ssh] on generating keys and adding them to your accout.

[github-ssh]: https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent

## Homebrew

Install Homebrew. When prompted, enter your administrator password and press Enter to create necessary directories.

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Homebrew [project](https://brew.sh)

## git

```sh
brew install git

# Global git ignore
echo ".DS_Store" >> ~/.gitignore_global
git config --global core.excludesfile ~/.gitignore_global

# User info
git config --global user.name "Firstname Lastname"
git config --global user.email your_email@host.tld
```

## Docker Desktop Community

As of the most recent update to this file, Docker Desktop for Apple Silicon Macs was in technical preview. The installer can be downloaded [here](https://docs.docker.com/docker-for-mac/apple-m1/).

For Intel-based Macs, download the latest [stable release](https://docs.docker.com/docker-for-mac/release-notes/) of Docker Desktop Community for Mac.

 Mount the .dmg and copy the application to `/Applications`. Launch Docker.app to complete installation.

## Visual Studio Code

Download [VS Code](https://code.visualstudio.com/Download) and extract it to `/Applications`

Useful extensions:

* Docker (ms-azuretools.vscode-docker)
* Dracula Official theme (dracula-theme.theme-dracula)
* Git History (donjayamanne.githistory)
* GitLens (eamodio.gitlens)
* Go (ms-vscode.go)
* Markdown All in One (yzhang.markdown-all-in-one)
* markdownlint (davidanson.vscode-markdownlint)
* PostgreSQL (ckolkman.vscode-postgres)
* Python (ms-python.python)
* Transformer (dakara.transformer)

Follow the [instructions](https://draculatheme.com/visual-studio-code/) to activate the theme in VS Code

## Python

```sh
# Install pyenv and pyenv-virtualenv
brew install pyenv pyenv-virtualenv

# Configure pyenv and pyenv-virtualenv
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
source ~/.zshrc

# List the available Python versions
pyenv install --list

# Install the latest Python 3
pyenv install 3.9.1

# Set the preferred order of Python interpreters
pyenv global 3.9.1 system

# Create and activate a Python virtual environment
pyenv virtualenv 3.9.1 sandbox-3.9.1
pyenv activate sandbox-3.9.1
```

pyenv [project](https://github.com/pyenv/pyenv)

pyenv-virtualenv [project](https://github.com/pyenv/pyenv-virtualenv)

pyenv global [docs](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md#pyenv-global-advanced)

## Ruby

```sh
# Install rvm
curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm

# List the available Ruby versions
rvm list known

# Install Ruby 2.6
rvm install 2.6

# On Apple Silicon:
CFLAGS="-Wno-error=implicit-function-declaration" rvm install 2.6

# Install Ruby documentation
rvm docs generate-ri
```

**WARNING: Ruby 2.7 made breaking changes - be cautious**

rvm [project](https://rvm.io)

## Node.js

```sh
# Install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash

# Configure installation and activate nvm
echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc
echo '[ -s "$NVM_DIR/nvm.sh ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm' >> ~/.zshrc
echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion' >> ~/.zshrc
source ~/.zshrc

# List the available Node.js versions
nvm ls-remote

# Install the latest Node.js 14.x (Fermiun)
nvm install lts/fermium
```

nvm [project](https://github.com/nvm-sh/nvm)

## Go

```sh
brew install go
```

## Java

### jenv

```sh
# Install jenv to enable switching between Java versions
brew install jenv
echo 'export PATH="$HOME/.jenv/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(jenv init -)"' >> ~/.zshrc
mkdir -p ~/.jenv/versions
```

jenv [project](https://github.com/jenv/jenv)

As of the most recent update to this file, OpenJDK builds for Apple Silicon are available from Azul, but not AdoptOpenJDK.

### Install Zulu OpenJDK 11 and configure jenv

Download the Java 11 for ARMv8 installer from the Zulu OpenJDK [project](https://www.azul.com/downloads/zulu-community/?os=macos&package=jdk). Mount the .dmg and run the installer package.

```bash
# Add OpenJDK 11 to jenv - enter password when prompted
jenv add /Library/Java/JavaVirtualMachines/zulu-11.jdk/Contents/Home

# Set a global Java version - takes effect on new shell
jenv global 11
```

### Install AdoptOpenJDK 8 & 11 and configure jenv

```sh
# Add AdoptOpenJDK as a source
brew tap AdoptOpenJDK/openjdk

# Install OpenJDK 8 and add to jenv - enter password when prompted
brew cask install adoptopenjdk8
jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-8.jdk/Contents/Home

# Install OpenJDK 11 and add to jenv - enter password when prompted
brew cask install adoptopenjdk11
jenv add /Library/Java/JavaVirtualMachines/adoptopenjdk-11.jdk/Contents/Home

# Set a global Java version - takes effect on new shell
jenv global 11
```

AdoptOpenJDK [project](https://github.com/AdoptOpenJDK/homebrew-openjdk)

### Install Maven & enable the jenv plugin

```sh
# Install Maven
brew install maven

# Install the Maven plugin for jenv
jenv enable-plugin maven
```

## IntelliJ

[Download](https://www.jetbrains.com/idea/download) the IntelliJ IDEA Community Edition installer for your Mac's architecture . Mount the .dmg and copy the application to `/Applications`.
