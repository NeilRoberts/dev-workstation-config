# macOS Dev Workstation Configuration

- [macOS Dev Workstation Configuration](#macos-dev-workstation-configuration)
  - [Overview](#overview)
  - [macOS System Settings](#macos-system-settings)
  - [Xcode Command Line Tools - if Xcode is unnecessary or inaccessible](#xcode-command-line-tools---if-xcode-is-unnecessary-or-inaccessible)
  - [Xcode](#xcode)
  - [Alfred](#alfred)
  - [Rectangle](#rectangle)
  - [iTerm 2](#iterm-2)
    - [Dracula Theme for iTerm](#dracula-theme-for-iterm)
  - [Oh My Zsh](#oh-my-zsh)
  - [SSH Key Pair](#ssh-key-pair)
  - [Homebrew](#homebrew)
  - [git](#git)
  - [Docker Desktop](#docker-desktop)
  - [Kubernetes](#kubernetes)
  - [Visual Studio Code](#visual-studio-code)
  - [Boost Note - Local](#boost-note---local)
  - [Python](#python)
  - [Node.js](#nodejs)
  - [Go](#go)
  - [Rust](#rust)
    - [Embedded Dev](#embedded-dev)
  - [Ruby](#ruby)
  - [Java](#java)
    - [jenv](#jenv)
    - [SDKMAN](#sdkman)
    - [Install Temurin 11 and configure jenv](#install-temurin-11-and-configure-jenv)
    - [Install Maven and enable the jenv plugin](#install-maven-and-enable-the-jenv-plugin)

## Overview

This documents the applications and tools that I've installed on my Macs for software development. The steps are mostly in order, but YMMV.

## macOS System Settings

- Enable tap to click
- Increase tracking speed
- Increase cursor size by one step
- Enable three-finger drag

## Xcode Command Line Tools - if Xcode is unnecessary or inaccessible

Install the Xcode Command Line Tools. When prompted, choose Install and Agree to the license agreement. **Apple Silicon:** if prompted to install Rosetta, do it.

```sh
xcode-select --install
```

## Xcode

Install Xcode from the Mac App Store. Launch, agree to the license agreement and enter password when prompted.

## Alfred

Download [Alfred](https://www.alfredapp.com), mount the DMG, and copy the application to `/Applications`. Launch, follow the steps to complete the setup, and configure the hotkey (`ctrl` double tap) and appearance (Alfred macOS Dark, Options: hide menu bar icon, use native macOS Dark Mode window rendering).

## Rectangle

Download [Rectangle](https://rectangleapp.com), mount the DMG, and copy the application to `/Applications`. Launch, follow the prompt to enable Accessibility, and select default shortcuts/behavior (Recommended).

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
# Scroll down to the plugins block, add "zsh-autosuggestions" (without quotes) to the space-separated list, and save the file

# Open a new shell
```

oh-my-zsh [project](https://github.com/ohmyzsh/ohmyzsh)

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

# Add Homebrew to PATH
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile

# Activate Homebrew in current terminal
eval "$(/opt/homebrew/bin/brew shellenv)"
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

## Docker Desktop

Download [Docker Desktop](https://docs.docker.com/desktop/mac/install) for your CPU architecture, mount the DMG, and copy the application to `/Applications`. Launch, follow the steps to complete setup and accept the terms.

## Kubernetes

Docker Desktop installs a version of `kubectl` and an engine, but `minikube` is preferred.

```sh
brew install minikube
```

## Visual Studio Code

Download [VS Code](https://code.visualstudio.com/Download) and extract it to `/Applications`

Useful extensions:

- Docker (`ms-azuretools.vscode-docker`)
- Dracula Official theme (`dracula-theme.theme-dracula`)
- Git Graph (`mhutchie.git-graph`)
- Git History (`donjayamanne.githistory`)
- GitLens (`eamodio.gitlens`)
- Kubernetes (`ms-kubernetes-tools.vscode-kubernetes-tools`)
- Makefile Tools (`ms-vscode.makefile-tools`)
- Markdown All in One (`yzhang.markdown-all-in-one`)
- markdownlint (`davidanson.vscode-markdownlint`)
- PostgreSQL (`ckolkman.vscode-postgres`)
- Thunder Client (`rangav.vscode-thunder-client`)
- Transformer (`dakara.transformer`)
- XML (`redhat.vscode-xml`)
- XML Tools (`dotjoshjohnson.xml`)
- YAML by RedHat (`redhat.vscode-yaml`)

Follow the [instructions](https://draculatheme.com/visual-studio-code/) to activate the theme in VS Code

## Boost Note - Local

Download [Boost Note - Local](https://github.com/BoostIO/BoostNote.next-local/releases), mount the DMG, and copy the application to `/Applications`.

## Python

```sh
# Install pyenv and pyenv-virtualenv
brew install pyenv pyenv-virtualenv

# Configure pyenv and pyenv-virtualenv
echo 'eval "$(pyenv init --path)"' >> ~/.zprofile
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
echo 'eval "$(pyenv virtualenv-init -)"' >> ~/.zshrc
source ~/.zshrc

# List the available Python versions
pyenv install --list

# Install the latest Python 3
pyenv install 3.10.3

# Set the preferred order of Python interpreters
pyenv global 3.10.3 system

# Open a new shell

# Example:
# Create an "aws" virtualenv and activate it
pyenv virtualenv 3.10.3 aws-3.10.3
pyenv activate aws-3.10.3

# Install some useful modules into the virtualenv
pip install awscli awscli-local

# Deactivate the virtualenv
pyenv deactivate
```

pyenv [project](https://github.com/pyenv/pyenv)

pyenv-virtualenv [project](https://github.com/pyenv/pyenv-virtualenv)

pyenv global [docs](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md#pyenv-global-advanced)

Useful VS Code extensions:

- AREPL for Python (`almenon.arepl`)
- Python (`ms-python.python`)

## Node.js

```sh
# Install nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

# Configure installation and activate nvm
echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc
echo '[ -s "$NVM_DIR/nvm.sh ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm' >> ~/.zshrc
echo '[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion' >> ~/.zshrc
source ~/.zshrc

# Install the latest LTS version of Node
nvm install --lts

# Upgrade to the latest version of NPM
nvm install-latest-npm

# Install the latest stable version of Node
nvm install node

# Upgrade to the latest version of NPM
nvm install-latest-npm

# Set the default version to the latest stable version of Node
nvm alias default node
```

nvm [project](https://github.com/nvm-sh/nvm)

Useful VS Code extensions:

- ESLint (`dbaeumer.vscode-eslint`)

## Go

```sh
brew install go

# Configure installation
mkdir $HOME/go
echo 'export GOPATH=$HOME/go' >> ~/.zshrc
echo 'export PATH=$PATH:$GOPATH/bin' >> ~/.zshrc

# For gRPC development
brew install bufbuild/buf/buf
```

Useful VS Code extensions:

- Buf (`bufbuild.vscode-buf`)
- Go (`golang.go`)

## Rust

```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

Rust [project](https://www.rust-lang.org)

rustup [installer](https://rustup.rs)

Useful VS Code extensions:

- rust-analyzer (`rust-lang.rust-analyzer`)

### Embedded Dev

```sh
brew install openocd
brew install arm-none-eabi-gdb
brew install arm-none-eabi-binutils
```

Embedded-specific VS Code extensions:

- Arm Embedded Debugger (`arm.embedded-debug`)
- Cortex-Debug (`marus25.cortex-debug`)
- Embedded Tools (`ms-vscode.vscode-embedded-tools`)

## Ruby

```sh
# Install latest rvm to get access to newer Rubies - may prompt for password if Ruby must be built from source
curl -sSL https://get.rvm.io | bash -s master
source ~/.rvm/scripts/rvm

# Install the supporting package first
brew instal shared-mime-info

# List the available Ruby versions
rvm list known

# Install Ruby 3.1 and documentation
rvm install ruby-3.1
rvm docs generate-ri

# Update the bundle gem and Ruby debug helper globally
gem install bundler
gem install debug

# Set the default Ruby version
rvm --default use 3.1
```

rvm [project](https://rvm.io)

Useful VS Code extensions:

- Cucumber (`cucumberopen.cucumber-official`)
- RubyLSP (`shopify.ruby-lsp`)

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

### SDKMAN

```sh
# Install SDKMAN!
curl -s "https://get.sdkman.io" | bash

# Restrict installable JDKs to Apple Silicon native versions
nano ~/.sdkman/etc/config

# If Rosetta2 compatibility is set to true, change it to false
sdkman_rosetta2_compatible=false

# Save the file and restart the terminal for changes to takes effect
```

SDKMAN! [project](https://sdkman.io)

### Install Temurin 11 and configure jenv

AdoptOpenJDK [became part of the Eclipse Foundation][eclipse-transition] and rebranded as Adoptium. Their OpenJDK releases are branded as Temurin.

[eclipse-transition]: https://blog.adoptopenjdk.net/2021/03/transition-to-eclipse-an-update/

```sh
# List the available JDKs
sdk list java

# Install Temurin 11 and add to jenv - enter password if prompted
sdk install java 17.0.8-tem
jenv add ~/.sdkman/candidates/java/17.0.8-tem

# Set a global Java version - takes effect on new shell
jenv global 17.0

# Reload zsh configs
source ~/.zshrc
```

Temurin 17 [releases](https://adoptium.net/temurin/releases/?version=17)

### Install Maven and enable the jenv plugin

```sh
# Install Maven
brew install maven

# Install the Maven plugin for jenv
jenv enable-plugin maven
```

Maven [project](https://maven.apache.org)

Useful VS Code extensions:

- Extension Pack for Java (`vscjava.vscode-java-pack`)
