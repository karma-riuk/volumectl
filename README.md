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
without it but it's uselful if you want to customise it), you need to install
the [read_ini.sh](https://raw.githubusercontent.com/rudimeier/bash_ini_parser/master/read_ini.sh) script.

You can do it in two different ways:

##### Downlading the script directly
```bash
mkdir -p $HOME/.local/lib
wget -O $HOME/.local/lib/read_ini.sh https://raw.githubusercontent.com/rudimeier/bash_ini_parser/master/read_ini.sh
chmod +x $HOME/.local/lib/read_ini.sh
```


### Installing the script


