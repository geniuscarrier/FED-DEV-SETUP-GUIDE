# Front End Development Setup Guide - Mac
This guide will help you install the most basic packages and command line tools that are needed for front end development on a Mac.

## Terminal
* Download [iTerm2] (http://iterm2.com/)
* Install [on-my-zsh] (http://ohmyz.sh/)
```bash
> curl -L http://install.ohmyz.sh | sh
```
* Install [Homebrew] (http://brew.sh/index.html)
```bash
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```
* Install [fasd] (https://github.com/clvv/fasd/wiki/Installing-via-Package-Managers) 
```bash
> brew install fasd
```
* Add the following to .zshrc file
```
# Load fasd
eval "$(fasd --init auto)"

# Enable plugins
plugins=(git fasd history history-substring-search sublime)

# Example aliases
alias zshconfig="subl ~/.zshrc"
alias ohmyzsh="subl ~/.oh-my-zsh"

#hosts
alias hosts='subl /etc/hosts'

#cd
alias ..='cd ..'
alias ...='cd ~'

#ls
alias la='ls -la'

# apache 
alias apachestart="sudo apachectl start"
alias apachestop="sudo apachectl stop"
alias apacherestart="sudo apachectl restart"
alias apachevhosts='subl /etc/apache2/extra/httpd-vhosts.conf'
alias apacheconf='subl /etc/apache2/httpd.conf'
```
* [git alias] (https://github.com/robbyrussell/oh-my-zsh/blob/master/plugins/git/git.plugin.zsh) 

## Server - Apache
* Edit Apache config
```bash
> apacheconf
```
Uncomment line - enable PHP
```
LoadModule php5_module libexec/apache2/libphp5.so
```
Uncomment line - enable multiple websites
```
# Virtual hosts
Include /private/etc/apache2/extra/httpd-vhosts.conf
```
Uncomment line - enable alias
```
LoadModule vhost_alias_module
libexec/apache2/mod_vhost_alias.so
```
Change Default DocumentRoot
```
DocumentRoot "/Users/username/www"
<Directory "/Users/username/www”>
</Directory>
```
* Edit Apache virtual host
```bash
> apachevhosts
```
Add a virtual host
```
<VirtualHost *:80>
    ServerAdmin webmaster@dummy-host.example.com
    DocumentRoot "/Users/username/www/example"
    ServerName local.example.com
    ServerAlias www.local.example.com
    ErrorLog "/private/var/log/apache2/local.example.com-error_log"
    CustomLog "/private/var/log/apache2/local.example.com-access_log" common
</VirtualHost>
```
* Edit hosts
```bash
> hosts
```
Add a host
```
127.0.0.1   local.example.com
```
* Restart Apache:
```
> apachestart
```

## Server - Node.js
* Install [Node] (http://nodejs.org/)

## Git
* Install Git
```bash
> brew install git
```
to verify
```bash
> which git
/usr/local/bin/git
```
* Config global git. Run the following commands
```bash
> git config --global user.name "YOUR_NAME"
> git config --global user.email YOUR_EMAIL
> git config --global core.editor "subl -n -w"
> git config --global core.excludesfile ~/.gitignore_global
> git config --global merge.tool Kaleidoscope
> git config --global diff.tool Kaleidoscope
```
to verify
```bash
> git config --list
user.name=YOUR_NAME
user.email=YOUR_EMAIL
core.excludesfile=/Users/your_name/.gitignore_global
core.editor=subl
merge.tool=Kaleidoscope
diff.tool=Kaleidoscope
```
to verify .gitconfig
```bash
> cat .gitconfig
[user]
    name = YOUR_NAME
    email = YOUR_EMAIL
[core]
    excludesfile = /Users/your_name/.gitignore_global
    editor = subl
[merge]
    tool = Kaleidoscope
[diff]
    tool = Kaleidoscope
```
* Edit .gitignore_global
```
.sass-cache
.DS_Store
```

## SASS & Compass
* Install Ruby via Homebrew
```bash
> brew install ruby
```
* Install SASS
```bash
> gem install sass
```
* Install Compass
```bash
> gem update --system
> gem install compass
```
* To verify
```bash
> sass -v
> compass -v
```

## Grunt
* Install Grunt's command line interface (CLI) globally
```bash
> npm install -g grunt-cli
```
* Change to the project's root directory. Create package.json
```bash
> npm init
```
* Install project dependencies locally with npm install.
```bash
> npm install grunt grunt-contrib-copy grunt-contrib-cssmin grunt-contrib-htmlmin grunt-contrib-jshint grunt-contrib-uglify grunt-contrib-concat grunt-contrib-imagemin grunt-contrib-watch grunt-contrib-sass grunt-contrib-compass grunt-contrib-clean grunt-usemin --save-dev
```
To verify npm packages has been installed successfully, see package.json:
```js
  "devDependencies": {
    "grunt": "^0.4.5",
    "grunt-contrib-clean": "^0.6.0",
    "grunt-contrib-compass": "^1.0.1",
    "grunt-contrib-concat": "^0.5.0",
    "grunt-contrib-copy": "^0.7.0",
    "grunt-contrib-cssmin": "^0.10.0",
    "grunt-contrib-htmlmin": "^0.3.0",
    "grunt-contrib-imagemin": "^0.9.2",
    "grunt-contrib-jshint": "^0.10.0",
    "grunt-contrib-sass": "^0.8.1",
    "grunt-contrib-uglify": "^0.6.0",
    "grunt-contrib-watch": "^0.6.1",
    "grunt-usemin": "^3.0.0"
  }
```
and check node_modules folder in project's root directory.
* To uninstall node module locally, run
```bash
> npm uninstall module_name
```
Or delete node_modules folder from the project directory.
* Create [Gruntfile.js] (http://gruntjs.com/getting-started)
* Run Grunt
```bash
> grunt
```
* To view global npm packages
```bash
> npm ls -g --depth=0
```
* To install node packages globally
```bash
> npm install -g package_name
```
It's located at /usr/local/lib/node_modules
* To remove node packages globally
```bash
> npm uninstall -g package_name
```

## Bower
* Install Bower
```bash
> npm install -g bower
```

## Editor - Sublime
* Install [Sublime] (http://www.sublimetext.com/)
* Install [Sublime Package Manager] (https://packagecontrol.io/)
* Install the following packages via package manager

1. Dotfiles Syntax Highlighting
2. Editor Config
3. SASS
4. Syntax Highlighting for Sass
5. DocBlockr
6. BracketHighlighter
7. Git Config
8. Markdown Editing
9. Markdown Preview
10. jade

## MongoDB
* Install MongoDB
```bash
> brew update
> brew install mongodb
```
* Go to home folder. Create a data folder:
```bash
> sudo mkdir -p /data/db
> sudo chown `id -u` /data/db
```
* Run MongoDB
```bash
> mongod
```
Open browser and go to [http://localhost:27017/] (http://localhost:27017/)
```bash
> mongod --rest
```
Open browser and go to [http://localhost:28017/] (http://localhost:28017/)
* Use mongo Shell
```bash
> mongo
```
