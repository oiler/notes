
## New computer account setup
```
ssh-keygen -t ed25519 -C "YOUR EMAIL"
eval "$(ssh-agent -s)"
touch ~/.ssh/config

    Host *
      AddKeysToAgent yes
      UseKeychain yes
      IdentityFile ~/.ssh/id_ed25519

ssh-add -K ~/.ssh/id_ed25519
ssh -T git@github.com
```


## Remote Server Git Setup

### Apache

Assumptions
* repo name = 'example'
* site domain name = 'example.com'
* Apache usr account that owns the files is `git`
* Apache html folder is `/var/www/`
* Apache site folder is `/var/www/example.com/public_html`
* The results of this guide will result in:
    * Your project files will live in `/var/www/example.com/public_html`
    * Your git repo will live in `/var/www/example.com/example.git`

Step by Step Guide
* cd to site's root folder
    > `cd /var/www/example.com`
* initiate the git repo
    > `git init --bare example.git`
* cd into the 'hooks' directory of your new repo
    > `cd example.git/hooks`
* create a new file (with nano or whatever) named  'post-receive'
    > `nano post-receive`
* paste into your new post-receive file the following
```
#!/bin/bash
while read oldrev newrev refname
do
    branch=$(git rev-parse --symbolic --abbrev-ref $refname)
    GIT_WORK_TREE=/var/www/example.com/public_html git checkout $branch -f
done
```
* save and exit out of the file
* update the file permissions 
    > `chmod 755 post-receive`

On Your Local Machine
* Your remote is now ready to be set, we'll call is 'prod'
    > `git remote add prod git@example.com:/var/www/example.com/example.git/`


