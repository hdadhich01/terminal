# 📜 Look like a 10x Developer Guide
Learn how to set up a **clean, minimal, and efficient** terminal geared towards **Python development**. This tutorial assumes a [Windows 10](https://www.microsoft.com/en-us/windows/get-windows-10)/[11](https://www.microsoft.com/en-us/windows/get-windows-11)  (preferably with the latest update) and [Visual Studio Code](https://code.visualstudio.com/) installation.

---
- [📜 Look like a 10x Developer Guide](#-look-like-a-10x-developer-guide)
  - [⌨️ Visual Studio Code](#️-visual-studio-code)
  - [🪟 WSL](#-wsl)
    - [⤵️ Install](#️-install)
    - [💡 Enable](#-enable)
  - [🐧 Ubuntu](#-ubuntu)
    - [⤵️ Install](#️-install-1)
  - [▶️ Terminal](#️-terminal)
    - [Setup](#setup)
    - [⚙️ Configuration](#️-configuration)
      - [📜 zsh](#-zsh)
      - [🐍 Python](#-python)
      - [📦 PDM](#-pdm)
    - [📄 Neofetch](#-neofetch)
    - [🏁 Finish](#-finish)
      - [❓ Errors](#-errors)
  - [👁️‍🗨️ Extra](#️️-extra)
    - [📂 Ubuntu File System](#-ubuntu-file-system)
    - [🎨 Change zsh Theme](#-change-zsh-theme)
    - [🔧 More Tools](#-more-tools)
      - [🤖 pipreqs](#-pipreqs)
      - [🚧 pre-commit](#-pre-commit)
      - [🕧 WakaTime](#-wakatime)
---

## ⌨️ Visual Studio Code
We will be using the most popular code editor out today. Go ahead and install the following extensions for future development.
* [Remote - WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) - Use the virtual environment and terminal within your projects
* [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) - Well how else will you work on Python projects

## 🪟 WSL
As per the official Microsoft description, "The Windows Subsystem for Linux lets developers run a GNU/Linux environment." Put into simple terms, you can use a Linux environment without waiting an hour for your dual-boot or VM configuration to load or risk your entire drive trying to partition it. Still confused? Check out this [video](https://www.youtube.com/watch?v=-atblwgc63E).

### ⤵️ Install
Open up a terminal (Command Prompt, PowerShell, Windows PowerShell) and run
```pwsh
wsl --install
wsl --set-default-version 2
```
We'll be using WSL 2, since its supposedly its faster. You can check out the official [Microsoft Comparison](https://docs.microsoft.com/en-us/windows/wsl/compare-versions) if you care. Once installation is finished, go ahead and reboot your computer. Relax, it's the only time you'll ever have to.

### 💡 Enable
Now a simple installation isn't enough, because complication is essential.
- Find `Turn Windows features on or off` through the Windows search bar
- Enable `Windows Subsystem for Linux` if it isn't already

## 🐧 Ubuntu
The most popular and beginner-friendly Linux distribution out there, Ubuntu, has collaborated with Microsoft to make WSL possible. This is the Linux distribution that we'll be running atop WSL.

### ⤵️ Install
Nothing crazy on this one, just install from the [Microsoft Store](https://apps.microsoft.com/store/detail/ubuntu/9PDXGNCFSCZV). Once finished, enter Ubuntu through the Windows search bar. It'll bring up a terminal and start installing the distribution. 

Once finished, you'll be prompted to enter a username, which you can just set to your Windows username, or whatever you like. Same goes for your password, although it's advisable to keep this the same as your Windows password so you don't have to reach for a sticky note or use your brain every time.

If you're **confused why your keyboard isn't outputting** to the screen when typing your password, this is an intentional feature to keep your credentials private.

## ▶️ Terminal
Now you can exit out of that ugly looking default Ubuntu terminal. Go ahead and open up Windows Terminal through your Windows search bar, and pin it to your taskbar if you so choose. You may have to install it from the [Microsoft Store](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701) due to what version you're on (specific releases of Windows 10.)

### Setup
Since we don't want PowerShell opening up with its generic color scheme, we're going to change it up.
* Click the dropdown by the `+` symbol and go to `Settings`, or do <kbd>Ctrl</kbd> + <kbd>,</kbd>
* In the `Startup` tab
  * Change your `Default profile` to `Ubuntu` (with the orange logo)
  * Make sure you hit `Save` on the bottom right (easy to forget)
* In the `Defaults` > `Appearance` tab
  * Set your `Color Scheme` to `One Half Dark`
  * Set your `Cursor shape` to `Filled box`
  * Set your `Background opacity` to `50%`
  * Set your `Enable acrylic material` to `on`
  * Again, make sure you hit `Save`
  * If you hate this appearance, then change it

Now you can exit out of the entire thing, and re-open it to something that hopefully doesn't look like it belongs to a systems engineer that spends his vacation in the company's server room.

### ⚙️ Configuration
Now for the most technical part of the guide, we'll set up your terminal to mimic that of a professional. I'll try my best to explain what the hell the commands you are punching in do.

Don't worry, you're not touching with any Windows system files here. If you mess up and have a panic attack, you can go to `Add or remove programs` through your Windows search bar, search for `Ubuntu` and click `⋮`. If you want to persevere, go to `Advanced options` and hit `Reset`, then you can pick up right back here. Otherwise, just uninstall and go use Repl.it or something.

#### 📜 zsh
We'll install everything involving the look and functionality of your terminal. Starting off, we'll upgrade everything because why not. It'll ask for your password because we are running it with `sudo`, which means "super user do."
```bash
sudo apt update && sudo apt upgrade
```
`update` just retrieves new versions of updatable packages, `upgrade` actually upgrades them. This command could take a while, so go make a cup of coffee.

Now we'll install `zsh` (a shell built on bash, the Ubuntu default) and `oh-my-zsh` (a customization framework for `zsh`). **Don't forget to indicate `yes` when it prompts you to make zsh your default shell.**
```bash
sudo apt install zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Now we'll install our theme. This is seperate from what we did back on Windows Terminal settings because we are modifying how the terminal actually displays informational text. 

This theme is called [Common](https://github.com/jackharrisonsherlock/common) and is "simple, clean and minimal" as per its author. You can get a different theme once you're through the guide and watched a YouTube tutorial on how to do so.
```bash
wget -O $ZSH_CUSTOM/themes/common.zsh-theme https://raw.githubusercontent.com/jackharrisonsherlock/common/master/common.zsh-theme
```
Now we'll install some plugins, stuff that'll make your life easier.
```bash
sudo apt install bat
echo "alias bat=/usr/bin/batcat" >> ~/.zshrc
sudo apt install tig
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/agkozak/zsh-z ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-z
code ~/.zshrc
```
Everything except the `echo` and last command fetches a plugin. The echo command sets an alias as `bat` for the plugin's default command, `batcat`. The last one gets tools for Visual Studio Code and opens up a file called `.zshrc`. This is the configuration file that `oh-my-zsh` executes on startup of every session.

Do a quick <kbd>Ctrl</kbd> + <kbd>F</kbd> and find `ZSH_THEME` to modify it to the following
```zshrc
ZSH_THEME="common"
```
Do another quick <kbd>Ctrl</kbd> + <kbd>F</kbd> and find `plugins` to modify it to the following
```bash
plugins=(copybuffer copypath copyfile dirhistory git jsontools tig web-search zsh-autosuggestions zsh-syntax-highlighting zsh-z)
```
The reason we have more plugins in addition to the ones we installed is because `oh-my-zsh` comes with some default ones, which we are simply enabling. You can see browse the functionalities of these plugins through the following: [Article](https://safjan.com/top-popular-zsh-plugins-on-github-2021/) | [Master list](https://github.com/unixorn/awesome-zsh-plugins) | [Oh My Zsh Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)

Once you've saved `.zshrc` and exited the window, you can run the following to reload the shell.
```bash
source ~/.zshrc
```
#### 🐍 Python
Now you have a nice shiny terminal, but you actually install language-specific tools rather than just have it open to make you feel like you'll work at FAANG some day.

Ubuntu already comes with Python, but it's not the latest, which is why we're going to go ahead and upgrade. The commands below are sourced from this [article](https://cloudbytes.dev/snippets/upgrade-python-to-latest-version-on-ubuntu-linux) because I'm not a Linux expert. Ubuntu doesn't offer the latest version as an option, so we're going to be importing from a [remote source](https://launchpad.net/~deadsnakes/+archive/ubuntu/ppa).
```bash
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt install python3.10
```
Now we have two versions installed. You can check your old version python3 by running `python3 -V`. **Before running the following**, replace the `x` with your old version's minor number (e.g., `Python 3.8.10` -> `8`). For the last command, make sure your current selection is `3.10`, otherwise select it.
```bash
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.x 1
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.10 2
sudo update-alternatives --config python3
```
Since we now have something new installed, something else will stop working due to the beauty of linux distributions. This "something" is `pip`, an essential package manager for Python. Run the following to patch up this issue.
```bash
sudo apt remove --purge python3-apt
sudo apt autoclean
sudo apt install python3-apt
sudo apt install python3.10-distutils
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
sudo python3.10 get-pip.py
sudo apt install python3.10-venv
sudo apt install build-essential
sudo apt install python3.10-dev
# another plugin
sudo pip install thefuck
echo "eval $(thefuck --alias)" >>  ~/.zshrc
```
Now you can run `python3` and see the latest version installed. However, typing that extra `3` seems pretty inconvenient, so we can add some aliases to the `.zshrc` file.
```bash
echo "alias py=/usr/bin/python3" >> ~/.zshrc
echo "alias python=/usr/bin/python3" >> ~/.zshrc
source ~/.zshrc
```
Go ahead and run `py` or `python` for the same results as before.

#### 📦 PDM
We installed `venv` in the previous section, so you could just run the following for the standard virtual environment setup inside your project directory.
```bash
python -m venv venv
source venv/bin/activate
```
However this directory will grow larger with your project over time. Each virtual environment can take up a lot of space with just the base install.

Enter [PDM](https://pdm.fming.dev/latest/), a package manager that takes advantage of [`PEP 582`](https://peps.python.org/pep-0582/) which allows Python to automatically recognize a `__pypackages__` directory in your project directory. Instead of having to activate a virtual environment every time, you can run your project as you normally would. In the background, Python uses the same global interpreter and imports packages from each project's `__pypackages__` directory. This enhancement is still pretty new, available in versions `3.8` and up. Using it puts you ahead of the game, and frankly, their interface is the most user-friendly I've ever used.

Once you're convinced, go ahead and run the following to install. **Make sure you run the `export` statement you're given upon installation.**
```bash
curl -sSL https://raw.githubusercontent.com/pdm-project/pdm/main/install-pdm.py | python3 -
pdm --pep582 >> ~/.zshrc
source ~/.zshrc
```
Visual Studio Code's Python extensions include linting tools that will display an error for imported packages they cannot find. This will happen because they do not automatically look inside your `__pypackages__` directory. `pdm-vscode` fixes this issue by generating a `settings.json` file in your workspace to help out your linter everytime you initialize a project. You can run the following to install.
```bash
sudo pip install -U pdm
pdm plugin add pdm-vscode
```
You can check out other `pdm` plugins you want to use [here](https://github.com/pdm-project/awesome-pdm). Also, I recommend the following resources to learn how to use `pdm`: [Documentation](https://pdm.fming.dev/latest/) | [Short](https://youtu.be/nHHB55QKu6g) | [Long](https://youtu.be/qOIWNSTYfcc)


### 📄 Neofetch
Installing a Linux distribution without Neofetch is something unheard of.  Rn the following so you can pull up some ASCII art and system information.
```bash
sudo apt install neofetch
exec zsh
neofetch
```
Running `wslfetch` returns a WSL-wary summary. You can also install Neofetch on Windows through a PowerShell terminal by running the following.
```pwsh
iwr -useb get.scoop.sh | iex
scoop install neofetch
scoop install git
neofetch
```
![Neofetch](https://i.ibb.co/HDyg1N4/Neofetch.jpg)

### 🏁 Finish
Upgrade everything and force reboot your distribution.
```bash
sudo apt update && sudo apt upgrade
sudo reboot -f
```

#### ❓ Errors
You might run into an error where you might have restarted your computer and open up your terminal to see the following layout, wondering where your original layout went.
```
wslg [ ~ ]$
```
To fix this, open up a PowerShell terminal and run the following.
```pwsh
wsl --shutdown
wsl
```
Now you can relaunch your terminal session to restore your original layout.
## 👁️‍🗨️ Extra
### 📂 Ubuntu File System
Ubuntu has its own file system where you can store your own projects. You can access your Windows file system, however it's recommended you place your projects in the `/home/` directory for more performance.
* `cd ~` will take you to your `/home/` directory
* `cd /` will take you to your root or `/` directory
* `/mnt` is the door to your Windows file system
  * `cd /mnt/c/Users/user/Desktop` lands you into `C:\Users\user\Desktop`

### 🎨 Change zsh Theme
If you didn't like the theme used in this guide, you can install another one per the steps below.
* Use a theme from the [internal library](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)
  * Run `code ~/.zshrc` > set `ZSH_THEME` to the theme's name > save, exit, and `source ~/.zshrc`
* Use a theme from the [external library](https://github.com/ohmyzsh/ohmyzsh/wiki/External-themes)
  * Install using `oh-my-zsh` instructions or `Ubuntu/Manual` if unavailable
  * Run `code ~/.zshrc` > set `ZSH_THEME` to the theme's name > save, exit, and `source ~/.zshrc`

change your theme
install wakatime

### 🔧 More Tools
#### 🤖 pipreqs
Sometimes you will start coding away, and when you finally reach the point of wanting to test it, you have to manually build your `requirements.txt` file with each package you import in your project. `pipreqs` will automatically go through your project directory files and fetch every imported module. Run the following to install it globally.
```bash
sudo pip install pipreqs
```
You can view the full [documentation](https://github.com/bndr/pipreqs) to add specific flags to suit your needs. Unfortunately, this module will generally import modules already present in the dependency lists of other modules. However, it's easier to delete those than manually adding your packages.

#### 🚧 pre-commit
Having to format your code manually by running commands every time before committing is pretty annoying. Run the following to install `pre-commit` globally.
```bash
sudo pip install pre-commit
```
Now obviously you wouldn't want `pre-commit` to run on every single project you are working on. This is why you have to run the following in your project's directory (that contains a `.git` file; has git instantiated). This installs a "pre-commit hook," or an action, that will run every time you commit.
```bash
pre-commit install
```
Now you can start integrating some [hooks](https://pre-commit.com/hooks.html) you want to use into a `.pre-commit-config.yaml` file that will executed before you commit. If you want contributors for your project, you should check out [pre-commit ci](https://pre-commit.ci/). This basically has the same functionality except that your contributors don't have to care about any of this stuff because it's all handled by the CI server. Check out its usage in this [simple project](https://github.com/hdadhich01/round-nutrition).

#### 🕧 WakaTime
Tracking how much time you are spending on your projects each day helps you develop a sense of priority and consistency. You can head over to [WakaTime](https://wakatime.com/) to set up an account.

As per the tools we used in this guide, you can set it up for [Visual Studio Code](https://wakatime.com/vs-code) and [zsh](https://wakatime.com/terminal). If you've got other editors, check out this [page](https://wakatime.com/plugins) to install their plugin. The instructions are pretty straightforward.
