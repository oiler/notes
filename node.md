Node
* single threaded
* uses an event-loop
* handles multiple concurrent operations well
* non-blocking from the start
	Cons
	* not for CPU intensive tasks
	* not for relational databases
		use a diff applicationa and node proxy to the web
when calling external source (ie, I/O), node apps run on single thread, so do one thing at a time. this is blocking. and why should avoid cpu heavy tasks.

call stack = last in / first out data structure

## install
```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.1/install.sh | bash
nvm install node
nvm use node
node -v
```

npm install --global gulp-cli


## setup
npm init
	creates package.json
package dependecies are _regular_ or _dev_

## help
`which node`
`which npm`

## packages
npm is a package manager, comes with Node
install packages locally or globally
local: ./node_modules
global: /

[nodemon](http://nodemon.io/)
	utility that monitors your app, and restarts when there are changes
	$ nodemon myapp.js
[eslint](http://eslint.org/docs/user-guide/configuring)

## [debug](https://nodejs.org/api/debugger.html)
add breakpoints with `debugger;`
and run via `node debug`
	inside debug console:
		help, c, repl

## [inspector](https://github.com/node-inspector/node-inspector)
`npm install -g node-inspector`
`node-debug` and open in browser

use `let` instead of `var`
var has global, function scope
let has limited scope (ES6)




## modules
three types of modules: core, file, npm
* core: provided by node, use reserved names ([list of names](https://nodejs.org/api/))
* file: user created, assigned to module.exports
* npm: work like core, but need to be installed via npm

can be imported in three different ways
* require('./filename') // relative path
* require('/home/folder/hello') // absolute path
* require('filename') // by name, in core lib or node_modules dir

each script has its own scope, and including one does not pollute the current scope
modules are cached automatically

## npm
install package globally, if local leave off -g flag
`npm install -g PACKAGE`
.gitignore you node_modules directory, there's no need to commit it since another user will get able to install when they setup (with npm install and package.json)
types of package save options
* `npm install --save PACKAGE` add as a dependency
* `npm install --save-dev PACKAGE` add as deploy dependency, ie wont be downloaded on production environment
* `npm install PACKAGE ^1.1` install until major release, so yes if 1.2, no if 2.0
* `npm install PACKAGE 1.1` install specific version
* `npm install PACKAGE ~1.1` install 1.1.* ??
* `npm install PACKAGE 1.1.x` install 1.1.*
* `npm install PACKAGE >1.1` install greater than 1.1
* `npm install PACKAGE >=1.1` install greater than or equal to 1.1
* `npm install PACKAGE <1.1` install less than 1.1
* `npm install PACKAGE <=1.1` install less than or equal to 1.1
* `npm install PACKAGE *` install any
* `npm install PACKAGE 1.1 latest` install according to 'latest" tag
update packages
`npm update --save`
list packages you have installed
`npm ls`
list view dependency tree options
`npm ls --depth=0`
list global packages
`npm ls -g`
check for outdated packages
`npm outdated`
uninstall
`npm uninstall PACKAGE`
to uninstall & remove as dependecy (from package.json)
`npm uninstall --save-dev PACKAGE`
`npm uninstall --save PACKAGE`
to get info about a specific package
`npm view PACKAGE`

## streams
https://nodejs.org/api/stream.html

## fs
https://nodejs.org/api/fs.html



### Examples
npm init
npm install --save-dev babel-preset-es2015
touch .babelrc
	{ "presets": ["es2015"] }
npm install --save-dev gulp
npm install --save-dev gulp-babel
touch .gulpfile.js



## rollup
https://github.com/rollup/rollup
