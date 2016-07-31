# bash

## notes
* `.bashrc` loaded by any shell, use to setup custom configs
* `.bash_profile` can do same as bashrc, is loaded once at login, use for user specific customizations
* OS X loads `.bash_profile` by default
* OS X run following to reload bash_profile  
$ `source ~/.bash_profile`
* comment syntax  
`# this is a comment`
* whitespace syntax, don't use spaces around equals sign  
good `hello="hello"`  
bad `hello = "hello"`

## variables
* no strict data types
* code:  
`my_project = "/var/www/html/my_project"`
* usage:  
$ `cd $my_project`

## aliases
* use as full command
* code:  
`alias gst='git status'`
* usage:  
$ `gst`

## functions
* params are positional, not required (ex, $1 $2 $3)
* `local` can be used inside function as private variable
* code:  
```shell
function gp() {  
    git push $1 $2
}
```
* usage:  
$ `gp origin master`

