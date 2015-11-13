# Drush Version Manager

DVM was inspired from NVM, RVM and PyEnv in that where so many versions of Drush and there's no convenient way to simply switch version in the way NVM, RVM and PyEnv have endeavored to achieve. With DVM joining the pack, the release of Drupal 8 and the popularity of a server configuration management tool Ansible I've essentially made this happen where there's no alternative program publicly available.

It's usage was intended for myself, but with a tool this convenient and cool there was no way I could keep it to myself.

## Installation

This script uses UNIX commands via Bash for ultimate compatibility and such requires a UNIX-based system.
It was made, tested and used on a OSX El Capitan system for intended use on a Debian environment for use with Vagrant.

### Ansible role

  An Ansible role has been made available for ease of implementation of Debian based systems: https://github.com/fubarhouse/fubarhouse.dvm

  This role can be found on the Galaxy at https://galaxy.ansible.com/detail#/role/5868

  This role was produced to work along-side [Jeff Geerling](https://twitter.com/geerlingguy)s' [DrupalVM](http://www.drupalvm.com/) and it works well for that purpose.

### Methods

The preferred method is to use the `$PATH` variable and `git`

    git clone https://github.com/fubarhouse/dvm.git ~/.dvm
    echo "export PATH=\$PATH:$HOME/.dvm" >> ~/.bash_profile;
    source ~/.bash_profile
    dvm install 7.0.0
    dvm use 7.0.0

Alternatively you can combine `alias` and `git`:

    git clone https://github.com/fubarhouse/dvm.git ~/.dvm
    alias dvm="${HOME}/.dvm/dvm" >> ~/.bash_profile;
    alias drush="${HOME}/.dvm/drush" >> ~/.bash_profile;
    source ~/.bash_profile
    dvm install 7.0.0
    dvm use 7.0.0

If you prefer to have a fixed install not using `git`, you can use any choice of the above including wget:

    mkdir "${HOME}/.dvm"
    wget -O ~/.dvm https://raw.githubusercontent.com/fubarhouse/dvm/master/dvm
    alias dvm="${HOME}/.dvm/dvm" >> ~/.bash_profile;
    alias drush="${HOME}/.dvm/drush" >> ~/.bash_profile;
    source ~/.bash_profile
    dvm install 7.0.0
    dvm use 7.0.0

And then you can ensure all the dependencies (composer, unzip etc) are installed using:

    dvm initialize

Initialization must use sudo and dependencies include a default Drush installation (installed at ~/dvm/) using composer, but it won't take long.

Dependencies not installed via the initialization argument (currently) include:

* wget

### Upgrading/updating

There's a convenient way of moving between versions of DVM without having to simply use git commands.

Upgrading will move you to the latest version and perform a git pull if you aren't on the latest version and it will perform a git pull if you're using the master copy.

    dvm upgrade

To interchange versions of DVM, you can use the following examples to demonstrate how you can do that:

    dvm upgrade 1.1
    dvm upgrade master

If you feel the need to switch between branches, you can simply use the following and substitute `master` for the version number

    cd ~/.dvm && git checkout master && git pull;

## Usage

To get a list of available versions:

    dvm ls-remote

Or to search for a version, type an argument to ls-remote to do a basic query string on the same set of commands:

    dvm ls-remote 8.0.0

To download and install version v7.0.0 and v8.0.0-rc3, do this:

    dvm install 7.0.0
    dvm install 8.0.0-rc3

You can switch between installed versions:

    dvm use 7.0.0
    dvm use 8.0.0-rc3

Or you can just run a command using a specific version of Drush using:

    dvm exec 7.0.0 --version

## Compatibility

### Drush version Manager

Only OSX and Ubuntu (CLI) systems are supported at this time, but any UNIX system should support it.

### Drush

Versions `2.x.x*` and later are successfully working without errors using DVM.

Versions `2.x.x+*` and `2.x.x` do not support global functionality, so it's recommended to use `3.x.x` at a minimum.

Versions `1.x.x+x` will not be officially supported as these versions do not support global functionality.

## License

dvm is released under the MIT license.

Copyright (C) 2015-2020 Karl Hepworth

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Compatibility Issues

`dvm` was made for use by OSX, Ubuntu and UNIX systems, and supports no other platform at this time.

## Problems

There are no known errors.

Still early days for this one, but there're questions about what we could do with this micro-app so time will tell.
