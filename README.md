# Volumectl
A small script that bundles volume control and dunst notification. Intended to be used either on command line or for keyboard shortcuts.


## Installation

### Dependencies

#### Dunst
Before installing and using this script, you will need to install the official 
[dunst](https://wiki.archlinux.org/title/Dunst) package.
Make sure you have the `dunstify` command available, that's what is needed to
have a nice looking percentage bar.

#### Bash Ini Reader

In order to use a custom config file (which is optional, the script works
without it but it's useful if you want to customise it), you need to install the
[read_ini.sh](https://raw.githubusercontent.com/rudimeier/bash_ini_parser/master/read_ini.sh)
script from the [bash_ini_parser](https://github.com/rudimeier/bash_ini_parser)
github repo.

You can do it in two different ways downloading the script directly or cloning
the git repo (the script won't care which one you choose, it knows how to handle
both situations).

##### Option 1: Cloning the git repo
```bash
git clone https://github.com/rudimeier/bash_ini_parser $HOME/.local/lib/bash_ini_parser
```

##### Option 2: Downloading the script directly
Make sure you have `wget` installed first. It doesn't change much to do it this
way since the repo hasn't been updated in a while.

```bash
mkdir -p $HOME/.local/lib
wget -O $HOME/.local/lib/read_ini.sh https://raw.githubusercontent.com/rudimeier/bash_ini_parser/master/read_ini.sh
chmod +x $HOME/.local/lib/read_ini.sh
```


### Installing volumectl
To install this script, you can do it in a similar way as with the ini parser, you
can either clone the repo or download the script directly (this option is not recommended
because you might miss new features or bug fixes).

#### Option 1 (recommended): Cloning the repo
To make install the script, just clone this repo and then create a symlink to
`volumectl` in whatever directory you want (as long as it is in your `$PATH`
variable, so that the script will be executable from anywhere in the terminal,
see this [link](https://www.tecmint.com/set-path-variable-linux-permanently/)
for more info about the `$PATH` variable). 

```bash
git clone https://github.com/karma-riuk/volumectl $HOME/.local/lib/volumectl
mkdir -p $HOME/.local/bin # just to make sure that the ~/.local/bin directory exists
ln -s $HOME/.local/lib/volumectl $HOME/.local/bin/volumectl
```




