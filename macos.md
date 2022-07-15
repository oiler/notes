
## Finder - Show hidden files
```
defaults write com.apple.Finder AppleShowAllFiles true
```


https://github.com/zzolo/mac-dotfiles/blob/master/zzolo/install.sh


https://postgresapp.com
http://blog.apps.npr.org/2013/06/06/how-to-setup-a-developers-environment.html

##homebrew


brew cask list

brew search --casks


brew cask install google-chrome

https://github.com/Homebrew/homebrew-cask/blob/master/USAGE.md




mkvirtualenv --python "$(which python3)" p3_text


which python3
python3 --version


https://wsvincent.com/install-django-python3-pip-virtualenv-virtualenvwrapper/
https://wsvincent.com/install-python3-mac/
python3 -m venv ~/.virtualenvs/myvenv
source ~/.virtualenvs/myvenv/bin/activate
pip freeze
deactivate
rmvirtualenv myvenv
workon myvirtualenv

pip3 install Django
pip freeze



## SETUP 

### NODE via NVM

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install node
nvm install --lts
nvm use --lts
nvm cache clear
```

and if you need a specific version
```
nvm install 10.19.0
nvm alias default 10.19.0
```
other commands
```
nvm use 12
nvm uninstall 12
```



