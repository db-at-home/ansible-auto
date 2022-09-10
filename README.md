# Ansible on MacOS

This is just a note on getting Ansible on a MacOS Monterey host quick as possible.

## Install Homebrew

according to the web page https://brew.sh/

    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

## tmux for iterm2

Quick side note for iTerm2 users...

    brew install tmux

and do more with iTerm and remote sessions following these write ups:

    https://gitlab.com/gnachman/iterm2/-/wikis/TmuxIntegration
    https://gitlab.com/gnachman/iterm2/-/wikis/tmux-Integration-Best-Practices

## Monterey has python3 and pip3

System doesn't have the latest of either, but don't stomp the system python or pip. Add pyenv

    brew install pyenv xz

## brew results:

    > brew list
    ==> Formulae
    autoconf	ca-certificates	libevent	m4		ncurses		openssl@1.1	
    pkg-config	pyenv		readline	tmux		utf8proc	xz
    
    ==> Casks
    rectangle

Run this command to modify the env

    echo 'eval "$(pyenv init --path)"' >> ~/.zprofile
    echo 'eval "$(pyenv init -)"' >> ~/.zshrc
    
now check for this at end of ~/.zprofile

    eval "$(pyenv init --path)"

at end of ~/.zshrc:

    eval "$(pyenv init -)"

## install python 3.10.6 and pip and make it 'active'

   pyenv install 3.10.6
   pyenv global 3.10.6

## pyenv results:

    > pyenv versions
      system
    * 3.10.6 (set by ~/.pyenv/version)

## prepend to path in .zprofile

Add these to the .zprofile and source it

  path=('~/.local/bin' $path)
  export PATH
  
## install ansible

  pip install --upgrade --user pip
  pip install --user ansible

## which ansible

  which ansible
  ansible --version

## we can manage django and other things in virtualenvs

  pip install --user virtualenv

## pip results:

    > pip list
    Package      Version
    ------------ -------
    ansible      6.3.0
    ansible-core 2.13.3
    cffi         1.15.1
    cryptography 37.0.4
    distlib      0.3.6
    filelock     3.8.0
    Jinja2       3.1.2
    MarkupSafe   2.1.1
    packaging    21.3
    pip          22.2.2
    platformdirs 2.5.2
    pycparser    2.21
    pyparsing    3.0.9
    PyYAML       6.0
    resolvelib   0.8.1
    setuptools   63.2.0
    virtualenv   20.16.3


## django virtualenv

    > virtualenv -p 3.10.6 django
    > cd django
    > source bin/activate
    (django) ~/git/django > django-admin startproject mysite
    (django) ~/git/django > cd mysite    
    (django) ~/git/django/mysite >  python manage.py runserver

play with the url - ctrl-c when done

    (django) ~/git/django/mysite >  python manage.py startapp polls

as described in

    https://docs.djangoproject.com/en/4.1/intro/tutorial01/
    https://docs.djangoproject.com/en/4.1/intro/tutorial02/
    https://docs.djangoproject.com/en/4.1/intro/tutorial03/
    https://docs.djangoproject.com/en/4.1/intro/tutorial04/
    https://docs.djangoproject.com/en/4.1/intro/tutorial05/
    https://docs.djangoproject.com/en/4.1/intro/tutorial06/
    https://docs.djangoproject.com/en/4.1/intro/tutorial07/
...
    https://docs.djangoproject.com/en/4.1/intro/reusable-apps/
    https://docs.djangoproject.com/en/4.1/intro/whatsnext/
