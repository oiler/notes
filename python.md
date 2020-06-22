# Python

## New MacOS Setup

### 1) install `pyenv`
    
* in a sea of articles and tips for working with Python on a Mac, this is by far the best writeup and explanation I've found
* src: [https://opensource.com/article/19/5/python-3-default-mac](https://opensource.com/article/19/5/python-3-default-mac)
* here's the short summary:
```zsh
brew install pyenv
pyenv install 3.7.3
echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.zshrc
```
* once you have pyenv, there are options for running a project by project virtual environment


### 2a using `virtualenv`
* now that we have `pip` (via pyenv), we can use the python version that was activated and assigned to shell
* for each project, follow these three commands to install virtualenv, create the env in your current folder, and then activate your current env
* src: [https://docs.python-guide.org/dev/virtualenvs/](https://docs.python-guide.org/dev/virtualenvs/)
```zsh
pip install virtualenv
virtualenv env
source env/bin/activate
```

### 2b using `venv`
https://docs.python.org/3/library/venv.html


## Other Links:
* https://sayazamurai.github.io/python-vs-javascript/