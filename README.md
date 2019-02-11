# Mac OSX Dev Setup

This document describes how to configure a developer environment on Mac OSX. 

- [System Update](#system-update)
- [Homebrew](#homebrew)
- [Terminal](#terminal)
- [Powerline Fonts](#powerline-fonts)
- [iTerm2](#iterm2)
- [Git](#git)
- [Text Editor](#text-editor)
- [Node.js](#nodejs)
- [JSHint](#jshint)
- [SASS](#sass)
- [Projects folder](#projects-folder)
- [Apps](#apps)

## System update

First thing you need to do, on any OS actually, is update the system! For that: **Apple Icon > Software Update...**

## Homebrew

[Homebrew](http://brew.sh/) is a package manager for Mac OS.
Package managers make it easier to install and update applications and/or libraries. 
### Install

An important dependency before Homebrew can work is the **Command Line Tools** for **Xcode**. These include compilers that will allow you to build things from source. 

Enter `$ xcode-select --install` into the terminal to install.

Finally, we can install Hombrew. In the terminal paste the following line (without the `$`), hit **Enter**, and follow the steps on the screen:

    $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

One thing we need to do is tell the system to use programs installed by Hombrew (in `/usr/local/bin`) rather than the OS default if it exists. We do this by adding `/usr/local/bin` to your `$PATH` environment variable:

    $ echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile

Open a new terminal tab with **Cmd+T** (you should also close the old one), then run the following command to make sure everything works:

    $ brew doctor
    
### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

    $ brew install <formula>
        
To update Homebrew's directory of formulae, run:

    $ brew update
    
**Note**: I've seen that command fail sometimes because of a bug. If that ever happens, run the following (when you have Git installed):

    $ cd /usr/local
    $ git fetch origin
    $ git reset --hard origin/master

To see if any of your packages need to be updated:

    $ brew outdated
    
To update a package:

    $ brew upgrade <formula>
        
Homebrew keeps older versions of packages installed, in case you want to roll back. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

    $ brew cleanup

To see what you have installed (with their version numbers):

    $ brew list --versions

## Terminal

Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/).

In **Finder**, drag and drop the **iTerm** Application file into the **Applications** folder and launch it.

Let's just quickly change some preferences. In the tab **Profiles**, create a new one with the "+" icon, and rename it. Then, select **Other Actions... > Set as Default**. 

I personally like ZShell

When done, hit the red "X" in the upper left (saving is automatic in OS X preference panes). Close the window and open a new one to see the size change.


## Z Shell

Since we spend so much time in the terminal, we should try to make it a more pleasant and colorful place. [Zsh](http://sourabhbajaj.com/mac-setup/iTerm/zsh.html) makes dealing with configurations, plugins, and themese a lot nicer.

Install zsh using Homebrew: 

	$ brew install zsh

Install a framework to help manage your zsh configuration and improve your terminal experience, I use [Oh My Zsh](https://github.com/robbyrussell/oh-my-zsh).

Install Oh My Zsh

	$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

The installation script should set zsh to your default shell, but if it doesn't you can do it manually:

	$ chsh -s $(which zsh)
	
### Install Powerline Fonts

Many Oh My Zsh themes require installing [Powerline Fonts](https://github.com/powerline/fonts) in order to render properly. Install your font(s) of choice, I like to use Inconsolata for Powerline.

### Install a Theme
In order to enable a [theme](https://github.com/robbyrussell/oh-my-zsh/wiki/Themes), set ```ZSH_THEME``` to the name of the theme in your ```~/.zshrc```, before sourcing Oh My Zsh; for example: ```ZSH_THEME=robbyrussell```. If you do not want any theme enabled, just set ```ZSH_THEME to blank: ZSH_THEME=""```

## Git

What's a developer without [Git](http://git-scm.com/)? To install, simply run:

    $ brew install git
    
When done, to test that it installed fine you can run:

    $ git --version
    
And `$ which git` should output `/usr/local/bin/git`.

Let's set up some basic configuration. Download the [.gitconfig](https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig) file to your home directory:

    $ cd ~
    $ curl -O https://raw.githubusercontent.com/nicolashery/mac-dev-setup/master/.gitconfig

It will add some color to the `status`, `branch`, and `diff` Git commands, as well as a couple aliases. Feel free to take a look at the contents of the file, and add to it to your liking.

Next, we'll define your Git user (should be the same name and email you use for [GitHub](https://github.com/) and [Heroku](http://www.heroku.com/)):

    $ git config --global user.name "Your Name Here"
    $ git config --global user.email "your_email@youremail.com"

They will get added to your `.gitconfig` file.

To push code to your GitHub repositories, we're going to use the recommended HTTPS method (versus SSH). So you don't have to type your username and password everytime, let's enable Git password caching as described [here](https://help.github.com/articles/set-up-git):

    $ git config --global credential.helper osxkeychain
    
**Note**: On a Mac, it is important to remember to add `.DS_Store` (a hidden OS X system file that's put in folders) to your `.gitignore` files. You can take a look at this repository's [.gitignore](https://github.com/nicolashery/mac-dev-setup/blob/master/.gitignore) file for inspiration.
    
## Text Editor

With the terminal, the text editor is a developer's most important tool. There are a variety of text editors and themes to choose from, what you use basically comes down to personal preference. My favorite editors include:

- [Visual Studio Code](https://code.visualstudio.com/)
- [Sublime Text](http://www.sublimetext.com/)
- [Atom](https://atom.io/)

## Node.js

Install [Node.js](http://nodejs.org/) with Homebrew:

    $ brew update
    $ brew install node

### Npm usage

To install a package:

    $ npm install <package> # Install locally
    $ npm install -g <package> # Install globally

To install a package and save it in your project's `package.json` file:

    $ npm install <package> --save

To see what's installed:

    $ npm list # Local
    $ npm list -g # Global

To find outdated packages (locally or globally):

    $ npm outdated [-g]

To upgrade all or a particular package:

    $ npm update [<package>]

To uninstall a package:

    $ npm uninstall <package>

##JSHint

JSHint is a JavaScript developer's best friend. JSHint is a javascript linter that helps identify errors in your code.

Install JSHint via npm (global install preferred)

    $ npm install -g jshint

Follow additional instructions on the [JSHint Package Manager page]

## SASS

CSS preprocessors are becoming quite popular, the most popular processors are [LESS](http://lesscss.org/) and [SASS](http://sass-lang.com). Preprocessing is a lot like compiling code for CSS. It allows you to reuse CSS in many different ways. Let's start out with using SASS as a basic preprocessor.

### Install

To install SASS you have to use NPM / Node, which you installed earlier using Homebrew. In the terminal use:

    $ npm install sass --global

Note: the `--global` flag is optional but it prevents having to mess around with file paths. You can install without the flag, just know what you're doing.

You can check that it installed properly by using:

    $ sass --version

This should output some information about the compiler:

    1.17.0 compiled with dart2js 2.1.0

Okay, SASS is installed and running. Great! 

### Usage

There's a lot of different ways to use SASS. Generally I use it to compile my stylesheet locally. We will set up a function for this when we install webpack.

Read more about LESS on their page here: http://sasscss.org/

## Projects folder

This really depends on how you want to organize your files, but I like to put all my version-controlled projects in `~/Documents/Projects`.

## Apps

Here is a quick list of some apps I use, and that you might find useful as well:

- [Google Drive](https://drive.google.com/): File syncing to the cloud too! I use Google Docs a lot to collaborate with others (edit a document with multiple people in real-time!), and sometimes upload other non-Google documents (pictures, etc.), so the app comes in handy for that. **(Free for 5GB)**
- [Slack](https://slack.com/): Messaging app that allows you to quickly communicate with your team and supports markdown.
- [Last Pass](https://www.lastpass.com/): Allows you to securely store your login and passwords. Even if you only use a few different passwords (they say you shouldn't!), this is really handy to keep track of all the accounts you sign up for.
- [Macdown](https://macdown.uranusjr.com/): As a developer, most of the stuff you write ends up being in [Markdown](http://daringfireball.net/projects/markdown/). In fact, this `README.md` file (possibly the most important file of a GitHub repo) is writeen in Markdown.




