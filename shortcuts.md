# Trello Shortcuts

KEY | NAME
--- | ----
w | board menu
/ | focus on search box
c | archive
<> | move to adjacent list
f | open filter menu
x | clear filters
n | new card
t | edit title
e | quick edit
l | label
d | due date
m | members

## full list
https://trello.com/shortcuts

* * *

# Github Markdown

## Basic Non-Obvious Stuff
```
* italics
** bold
[text](link)
![embedded image link]
- [ ] tasks
* * * horizontal rule
```

## Tables
```
header1 | header2
------- | -------
a cell | another cell
more cells | final cell

```

## full list
https://guides.github.com/features/mastering-markdown/

* * *

# MySQL

## connect to local MAMP
Use a specific username and password
```
/Applications/MAMP/Library/bin/mysql --host=localhost -uroot -proot
```

* * * 

# WordPress

## local setup
```
define('FS_METHOD', 'direct');
```

* * * 

# General

## Time In Seconds

key | val
--- | ---
day | 86400
week | 604800
month | 2629000
year = 31536000

##  OS X hacks

Kill DNS Cache  
* `sudo killall -HUP mDNSResponder`

Kill screenshot sound
* `screencapture -x quiet.jpg`

Change screenshot file type
* `defaults write com.apple.screencapture type -string "png"`

Change screenshot file location
* `defaults write com.apple.screencapture location /folderlocation`

Show hidden files
* `defaults write com.apple.finder ShowAllFiles YES`

Show pathbar
* `defaults write com.apple.finder ShowPathbar -bool true`

Install python3
```
brew install python3 pipenv
python3 --version
pip3 --version
```

symlinks
* `ln -s EXISTING_FILE_OR_DIRECTORY SYMLINK_NAME`
* 'unlink SymLinkToRemove'

## google spreadsheet data
```
https://spreadsheets.google.com/feeds/list/PUT-KEY-HERE/od6/public/values?alt=json
```

## AWS CLI

### Setup

```
brew install awscli
aws --version
aws configure
```

### S3 upload public
```
aws s3 cp FILENAME s3://oiler/FOLDER/ --grants read=uri=http://acs.amazonaws.com/groups/global/AllUsers

```
[route53 dns guide](https://medium.com/@limichelle21/connecting-google-domains-to-amazon-s3-d0d9da467650)
[with cloudfront https](https://www.josephecombs.com/2018/03/05/how-to-make-an-AWS-S3-static-website-with-ssl)


### git commands

* push branch as master (looking at you, WPEngine)
```
git push stage branchname:master
```

* delete branch on a remote
```
git push origin --delete branchname
```


### github pages DNS settings

* create CNAME with your subdomain pointing to your github account: `oiler.github.io.`
* create A record pointing to one of github's servers:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```



