# Volumectl
A small script that bundles volume control and dunst notification. Intended to be used either on command line or for keyboard shortcuts.

Here below is a demonstration of how it works when pressing the volume and mute
keys. The behaviour of the notification is the same if the script was executed
from the terminal.
![demo](./volumectl_demo.gif)

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
Make sure you have `wget` installed first. 

Downloading the script directly doesn't change much to do it this way since the
repo hasn't been updated in a while.

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
for more info about the `$PATH` variable). In the commands below I'm using the
`$HOME/.local/bin`, which by default is **not** in the `$PATH` variable, so make
sure you set it.

```bash
git clone https://github.com/karma-riuk/volumectl $HOME/.local/lib/volumectl
mkdir -p $HOME/.local/bin # just to make sure that the ~/.local/bin directory exists
ln -s $HOME/.local/lib/volumectl $HOME/.local/bin/volumectl
```

#### Option 2 (not recommended): Downloading the script directly

```bash
mkdir -p $HOME/.local/bin
wget -O $HOME/.local/bin/volumectl https://raw.githubusercontent.com/karma-riuk/volumectl/master/volumectl
chmod +x $HOME/.local/bin/volumectl
```


## Usage

### Command line

To use the script, simply execute the `volumectl` with the flag you want,
example:
```bash
volumectl -i
```

#### Possible flags
(You can find all the information below by doing `volumectl -h`)

|Short flag | Equivalent long flag |Description|
|-----|-----|-----|
|`-i` | `--increase` | increases the volume by the "normal" amount (by default: 5%) |
|`-i <arg>` | `--increase <arg>` |  increase the volume by the `<arg>` amount |
|`-I` | `--big-increase` | increases the volume by the "big" amount (by default: 10%) |
|`-d` | `--decrease` | decreases the volume by the "normal" amount (by default: 5%) |
|`-d <arg>` | `--decrease <arg>` |  decrease the volume by the `<arg>` amount |
|`-D` | `--big-decrease` | decreases the volume by the "big" amount (by default: 10%) |
|`-s <arg>` | `--set <arg>` | sets the volume to `<arg>` |
|`-m` | `--mute` | activates mute |
|`-u` | `--unmute` | deactivates mute |
|`-t` | `--toggle` | toggles mute |
|`-g` | `--get-volume` | prints the current volume level |
|`-G` | `--get-mute` | prints the current mute state |


#### Optional flags
|Short flag | Equivalent long flag |Description|
|-----|-----|-----|
|`-c <file>` | `--config <file>` | use `<file>` as the config file instead of the default location (see below) |
|`-v` | `--verbose` | print each step the script passes through |
|`-h` | `--help` | print the help message and exit |

### Key Bindings

#### Awesomewm
Here is an example of how keybindings would look like in awesomewm (tested)

```lua
---- Volume Management
awful.key({ }, "XF86AudioMute",
          function ()
              awful.spawn("volumectl -t")
          end,
          {description = "Toggle mute", group = "Media management"}),

awful.key({ "Shift" }, "XF86AudioMute",
          function ()
              awful.spawn("volumectl -m")
          end,
          {description = "Set mute", group = "Media management"}),

awful.key({ }, "XF86AudioRaiseVolume",
          function ()
              awful.spawn("volumectl -i")
          end,
          {description = "Increase volume", group = "Media management"}),

awful.key({ "Shift" }, "XF86AudioRaiseVolume",
          function ()
              awful.spawn("volumectl -I")
          end,
          {description = "Increase volume a lot", group = "Media management"}),

awful.key({ }, "XF86AudioLowerVolume",
          function ()
              awful.spawn("volumectl -d")
          end,
          {description = "Decrease volume", group = "Media management"}),

awful.key({ "Shift" }, "XF86AudioLowerVolume",
          function ()
              awful.spawn("volumectl -D")
          end,
          {description = "Decrease volume a lot", group = "Media management"}),
```

#### i3

Here is an example of how keybindings would look like in awesomewm (**NOT TESTED**, please tell me if it's wrong)

```i3
bindsym XF86AudioMute exec --no-startup-id volumectl -t
bindsym Shift+XF86AudioMute exec --no-startup-id volumectl -m

bindsym XF86AudioRaiseVolume exec --no-startup-id volumectl -i
bindsym Shift+XF86AudioRaiseVolume exec --no-startup-id volumectl -I

bindsym XF86AudioLowerVolume exec --no-startup-id volumectl -d
bindsym Shift+XF86AudioLowerVolume exec --no-startup-id volumectl -D
```

## Config

The config file is an optional feature, but it allows you to set a different
volume controller than the default one ([pamixer](https://github.com/cdemoulins/pamixer))

To enable the config file, first make you installed the `read_ini.sh` script
(see above, in the dependencies) just create a `config.ini` file in the
`$XDG_CONFIG_HOME/volumectl` (`$HOME/.config/volumectl/` if `$XDG_CONFIG_HOME`
is not set) directory.

If you think the default values are fine but want to modify just one value,
then you can just place that value in the config file, `volumectl` will just
take that changed value and keep the rest as default.

You can see what all the available config variables are by looking at the
[example_config.ini](./example_config.ini).

The easiest way to go to setup a custom config is by running the following commands
```console
mkdir -p ${XDG_CONFIG_HOME:-$HOME/.config}/volumectl
cp $HOME/.local/lib/volumectl/example_config.ini ${XDG_CONFIG_HOME:-$HOME/.config}/volumectl/config.ini
```
and then editing the config with your prefered editor and tinker with it.

Quick tip: when tinkering with the config, be sure to use `volumectl -v` (it's
important to put the `-v` right after the command, so that you see everything
that's happening) so that you see what the values are for the variables and
will be able to spot where your error is, if there is any.





