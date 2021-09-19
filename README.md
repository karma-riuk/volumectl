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
script from the (bash_ini_parser)[https://github.com/rudimeier/bash_ini_parser]
github repo.

You can do it in two different ways downloading the script directly or cloning
the git repo (the script won't care which one you choose, it knows how to handle
both situations).

##### Cloning the git repo
```bash
git clone https://github.com/rudimeier/bash_ini_parser $HOME/.local/lib/bash_ini_parser
```

##### Downloading the script directly
```bash
mkdir -p $HOME/.local/lib
wget -O $HOME/.local/lib/read_ini.sh https://raw.githubusercontent.com/rudimeier/bash_ini_parser/master/read_ini.sh
chmod +x $HOME/.local/lib/read_ini.sh
```


### Installing volumectl


