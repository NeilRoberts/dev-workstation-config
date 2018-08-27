# dev-workstation-config
Notes on my workstation config - may not be safe for public consumption

#### Install Homebrew
Project [site](https://brew.sh)

    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"


#### Install pyenv
See the [installation instructions](https://github.com/pyenv/pyenv)

    brew update
    brew install pyenv

#### Install pyenv-virutualenv
See the [installation instructions](https://github.com/pyenv/pyenv-virtualenv)

    brew install pyenv-virtualenv

#### Install Python versions
    $ pyenv install 3.6.6
    $ pyenv install 3.7.0

Set the preferred order of Python versions:

    $ pyenv global 3.6.6 3.7.0 system

pyenv global [docs](https://github.com/pyenv/pyenv/blob/master/COMMANDS.md#pyenv-global-advanced)

#### Create and activate a virtualenv for Python 3.6

    $ pyenv virtualenv 3.6.6 py3.6
    $ pyenv activate py3.6
