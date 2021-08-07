# Activate pyenv environment automatically when entering a directory

 - Install `pyenv`
 - Create your own environment with `pyenv virtualenv <python-version> <env-name>` e.g. `pyenv virtualenv 3.7.4 termograph-3.7.4`
 - Run `pyenv local termograph-3.7.4`. This command will create a `.python-version` file
 - To ignore this file globally, add it to `~/.gitignore_global` and run `git config --global core.excludesfile ~/.gitignore_global`

 Every time you enter the directory where run `pyenv local ...`, pyenv will automatically activate the environment. It will also keep it activated in nested folders and it will deactivate when exiting

