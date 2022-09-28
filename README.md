# 📜 Look like a 10x Developer
Learn how to set up a **clean, minimal, and efficient** terminal geared towards **Python development**. This tutorial assumes a [Windows 10](https://www.microsoft.com/en-us/windows/get-windows-10)/[11](https://www.microsoft.com/en-us/windows/get-windows-11)  (preferably with the latest update) and [Visual Studio Code](https://code.visualstudio.com/) installation.

- [📜 Look like a 10x Developer](#-look-like-a-10x-developer)
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
  - [👁️‍🗨️ Information](#️️-information)
    - [📂 Ubuntu File System](#-ubuntu-file-system)
    - [🎨 Change zsh Theme](#-change-zsh-theme)
    - [🔧 More Tools](#-more-tools)
      - [🎥 asciinema](#-asciinema)
      - [🤖 pipreqs](#-pipreqs)
      - [🚧 pre-commit](#-pre-commit)
      - [🖊️ GPG](#️-gpg)
      - [🕛 WakaTime](#-wakatime)
  - [🏁 Finish](#-finish)
    - [❓ Errors](#-errors)

## ⌨️ Visual Studio Code
We will be using the most popular code editor out today and the following extensions for our
* [Remote - WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl) - Use the virtual environment and terminal within your projects
* [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) - Well how else will you work on Python projects

## 🪟 WSL
As per the official Microsoft description, "The Windows Subsystem for Linux lets developers run a GNU/Linux environment." Put into simple terms, you can use a Linux environment without waiting an hour for your dual-boot or VM configuration to load or risk your entire drive trying to partition it. Still confused? Check out this [video](https://www.youtube.com/watch?v=-atblwgc63E).

### ⤵️ Install
Open up PowerShell and run the following to install and modify the default version. We'll be using version `2` since it's supposedly faster. You can check out the official [Microsoft Comparison](https://docs.microsoft.com/en-us/windows/wsl/compare-versions) if you care.
```pwsh
wsl --install
wsl --set-default-version 2
```

### 💡 Enable
Now a simple installation isn't enough so you'll need to enable a feature.
- Make sure `Virtualization` is enabled in the `CPU` section of your task manager's `Performance` page
- Navigate to `Turn Windows features on or off` through the Windows search bar
- Enable `Windows Subsystem for Linux` if it isn't already

Now go ahead and reboot your computer. Relax, it's the only time you'll ever have to.

## 🐧 Ubuntu
The most popular and beginner-friendly Linux distribution out there, Ubuntu has collaborated with Microsoft to make WSL possible. This is the Linux distribution that we'll be running atop WSL.

### ⤵️ Install
Nothing crazy on this one, just install from the [Microsoft Store](https://apps.microsoft.com/store/detail/ubuntu/9PDXGNCFSCZV). Once finished, enter Ubuntu through the Windows search bar. It'll bring up a terminal and start installing the distribution.

Once finished, launch the app and run its installation course. Then you'll be prompted to enter a username, which you can just set to your Windows username, or whatever you like. Same goes for your password, although it's advisable to keep this the same as your Windows password so you don't have to reach for a sticky note or use your brain every time.

If you can't type out a username, or it's automatically set as `root`, run the following commands in PowerShell (retrieved from [issue](https://github.com/microsoft/WSL/issues/8736)) to briefly reinstall and enter your username.
```pwsh
wsl --unregister Ubuntu
ubuntu install --ui=none
```
If your **keyboard isn't outputting** to the screen while typing out your password, this is an intentional feature to keep your credentials private.

## ▶️ Terminal
Now you can exit out of that bland default Ubuntu terminal. Go ahead and open up Windows Terminal through your Windows search bar, and pin it to your taskbar if you so choose. You may have to install it from the [Microsoft Store](https://apps.microsoft.com/store/detail/windows-terminal/9N0DX20HK701) due to what version you're on (specific releases of Windows 10.)

### Setup
Since we don't want PowerShell and the generic color scheme opening up by default, we're going to change it up.
* Click the dropdown by the `+` symbol and go to `Settings` (or <kbd>Ctrl</kbd> + <kbd>,</kbd>)
* In the `Startup` tab
  * Change your `Default profile` to `Ubuntu` (with the orange logo)
  * Make sure you hit `Save` on the bottom right (easy to forget)
* In the `Defaults` > `Appearance` tab
  * Set your `Color Scheme` to `One Half Dark`
  * Set your `Background opacity` to `50%`
  * Set your `Enable acrylic material` to `on`
  * Again, make sure you hit `Save`
  * Modify however else you desire

Now you can exit out of the entire thing, and re-open it to something that hopefully doesn't look like it belongs to a systems engineer that spends his vacation in the company's server room.

### ⚙️ Configuration
Now for the most technical part of the guide, we'll set up your terminal to mimic that of a professional. I'll try my best to explain what the hell the commands you are punching in do.

Don't worry, you're not touching with any Windows system files here. If you mess up and have a panic attack, you can go to `Add or remove programs` through your Windows search bar, search for `Ubuntu` and click `⋮` > `Advanced options` > `Reset`.

#### 📜 zsh
We'll install everything involving the look and functionality of your terminal. Starting off, we'll upgrade everything because why not. It'll ask for your password because we are running it with `sudo`, which means "super user do." The `-y` flag answers `yes` to all `Y/n` prompts.
```bash
sudo apt update && sudo apt upgrade -y
```
`update` just retrieves new versions of updatable packages, `upgrade` actually upgrades them. This command could take a while, so go make a cup of coffee.

Now we'll install `zsh` (a shell built on bash, the Ubuntu default) and `oh-my-zsh` (a customization framework for `zsh`). **Don't forget to indicate `yes` when it prompts you to make zsh your default shell.**
```bash
sudo apt install zsh -y
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
Now we'll install our theme. This is seperate from what we did back on Windows Terminal settings because we are modifying how the terminal actually displays informational text. The theme we are installing is called [Typwritten](https://github.com/reobin/typewritten) and is a "minimal zsh prompt" as per its author. Learn how to install a different theme of your liking [here](#-change-zsh-theme).

The first command is retrieving the theme from its repository and the following commands set up symbolic links for it.
```bash
git clone https://github.com/reobin/typewritten.git $ZSH_CUSTOM/themes/typewritten
ln -s "$ZSH_CUSTOM/themes/typewritten/typewritten.zsh-theme" "$ZSH_CUSTOM/themes/typewritten.zsh-theme"
ln -s "$ZSH_CUSTOM/themes/typewritten/async.zsh" "$ZSH_CUSTOM/themes/async"
echo 'TYPEWRITTEN_CURSOR="block"' >> ~/.zshrc
echo 'TYPEWRITTEN_PROMPT_LAYOUT="singleline_verbose"' >> ~/.zshrc
```
Now we'll install some plugins, stuff that'll make your life easier. Everything except the `echo` and last command fetches a plugin. The echo command sets an alias as `bat` for the plugin's default command, `batcat`. The last one installs tools for [VS Code](#️-visual-studio-code) and opens up a file called `.zshrc`. This is the configuration file that `oh-my-zsh` executes on startup.
```bash
sudo apt install bat -y
echo "alias bat=/usr/bin/batcat" >> ~/.zshrc
sudo apt install tig
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/agkozak/zsh-z ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-z
code ~/.zshrc
```

Hit <kbd>Ctrl</kbd> + <kbd>F</kbd> and find `ZSH_THEME` to modify it to the following
```
ZSH_THEME="typewritten"
```
Hit another <kbd>Ctrl</kbd> + <kbd>F</kbd> and find `plugins` to modify it to the following
```
plugins=(copybuffer copypath copyfile dirhistory git jsontools tig web-search zsh-autosuggestions zsh-syntax-highlighting zsh-z)
```
The reason we have more plugins in addition to the ones we installed is because `oh-my-zsh` comes with some default ones, which we are simply enabling. You can browse the functionalities of these plugins through the following: [Article](https://safjan.com/top-popular-zsh-plugins-on-github-2021/) | [Masterlist](https://github.com/unixorn/awesome-zsh-plugins) | [Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)

Once you've saved `.zshrc` and exited the window, you can run the following to reload the configuration.
```bash
source ~/.zshrc
```
#### 🐍 Python
Now you have a nice looking terminal, but you actually need language-specific tools rather than having it open to make you feel like you'll work at FAANG some day.

The latest version of Ubuntu on the Windows Store includes Python `3.10`. You can make sure by running `python3 -V`. If you have a different version, check out this [article](https://cloudbytes.dev/snippets/upgrade-python-to-latest-version-on-ubuntu-linux) for instructions on how to upgrade (good luck). To install and manage project dependencies like any normal developer, you'll need package managing tools. Run the following to install `pip` and `venv`.
```bash
sudo apt install python3-pip -y
sudo apt install python3.10-venv -y
sudo apt install python-is-python3
```
You can make sure you have correctly installed `pip` by running `pip --version`. Typing out `python` can get a bit tedious, so let's configure an alias.
```bash
echo "alias py=/usr/bin/python3" >> ~/.zshrc
source ~/.zshrc
```
Run `py` or `python` to make sure you can enter the REPL. Run `exit()` to hop out.

#### 📦 PDM
We installed `venv` in the previous section, so you could just run the following for the standard virtual environment setup inside your project directory.
```bash
python -m venv venv
source venv/bin/activate
```
However this directory will grow larger with your project over time. Each virtual environment can take up a lot of space with just the base install.

Enter [PDM](https://pdm.fming.dev/latest/), a package manager that takes advantage of [`PEP 582`](https://peps.python.org/pep-0582/) which allows Python to automatically recognize a `__pypackages__` directory in your project directory. Instead of having to activate a virtual environment every time, you can run your project as you normally would. In the background, Python uses the same global interpreter and imports packages from each project's `__pypackages__` directory. This enhancement is still pretty new, available in versions `3.8` and up. Using it puts you ahead of the game, and frankly, their interface is the most user-friendly I've ever used.

Once you're convinced, install it and configure PEP 582 to enable it for dependency management for your projects.
```bash
curl -sSL https://raw.githubusercontent.com/pdm-project/pdm/main/install-pdm.py | python3 -
echo "export PATH=/home/$USER/.local/bin:\$PATH" >> ~/.zshrc && source ~/.zshrc
pdm --pep582 >> ~/.zshrc && source ~/.zshrc
```
[VS Code's](#️-visual-studio-code) Python extensions include linting tools that will display an error for imported packages they cannot find. This will happen because they do not automatically look inside your `__pypackages__` directory. `pdm-vscode` fixes this issue by generating a `settings.json` file in your workspace to help out your linter everytime you initialize a project. You can run the following to install.
```bash
pdm plugin add pdm-vscode
```
You can check out other `pdm` plugins you want to use [here](https://github.com/pdm-project/awesome-pdm). Also, I recommend the following resources to learn how to use `pdm`: [Documentation](https://pdm.fming.dev/latest/) | [Short](https://youtu.be/nHHB55QKu6g) | [Long](https://youtu.be/qOIWNSTYfcc)


### 📄 Neofetch
Installing a Linux distribution without Neofetch is something unheard of.  Run the following so you can pull up some ASCII art and system information.
```bash
sudo apt install neofetch -y
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

## 👁️‍🗨️ Information
### 📂 Ubuntu File System
Ubuntu has its own file system where you can store your own projects. You can access your Windows file system, however it's recommended you place your projects in the `/home/` directory for more performance.
* `cd`/`cd ~` will take you to your `/home/user` directory
* `cd /` will take you to your root or `/` directory
* `/mnt` is the door to your Windows file system
  * ex: `cd /mnt/c/Users/user/Desktop` = `C:\Users\user\Desktop`

Run `mkdir ~/dev` to make a `dev` folder in your landing directory (`/home/user`). It is recommended to have your projects stored here rather than your Windows file system for faster performance and avoiding compilation errors during package installment.

### 🎨 Change zsh Theme
If you didn't like the theme used in this guide, you can install another one per these steps:
* Use a theme from the [internal library](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)
  * Run `code ~/.zshrc` > set `ZSH_THEME` to the theme's name > save, exit, and `source ~/.zshrc`
* Use a theme from the [external library](https://github.com/ohmyzsh/ohmyzsh/wiki/External-themes)
  * Install using the `oh-my-zsh` or `Ubuntu/Manual` instructions
  * Run `code ~/.zshrc` > modify `ZSH_THEME` > save, exit, and run `source ~/.zshrc`

### 🔧 More Tools
#### 🎥 asciinema
Sometimes you want to layout the complete history of the commands you punched in to your terminal through a video. Setting up a screen recording software or making lengthy logs is inefficient. Instead, you can use [`asciinema`](https://asciinema.org/) to quickly record and upload sessions. Go ahead and make an account online and run the following to install it.
```bash
sudo apt-add-repository ppa:zanchey/asciinema -y
sudo apt-get update
sudo apt-get install asciinema
```
You can run the following to start recording, and run `exit` to stop recording.
```bash
asciinema rec
```
You can configure recordings to save to your account through the following command.
```bash
asciinema auth
```

#### 🤖 pipreqs
Sometimes you will start programming away, and when you finally reach the point of wanting to test it, you have to manually build your `requirements.txt` file with each package you import in your project. [`pipreqs`](https://github.com/bndr/pipreqs) will automatically go through your project directory files and fetch every imported module. Run the following to install it.
```bash
pip install pipreqs
```
You can view the full [documentation](https://github.com/bndr/pipreqs) to add specific flags to suit your needs. Unfortunately, this module will generally import modules already present in the dependency lists of other modules. However, it's easier to delete those than manually adding your packages.

#### 🚧 pre-commit
Having to format your code manually by running commands every time before committing is pretty annoying. Run the following to install [`pre-commit`](https://pre-commit.com/) globally.
```bash
pip install pre-commit
```
Now obviously you wouldn't want it to run on every single project you are working on. This is why you have to run the following in your project's directory (that contains a `.git` folder; has git instantiated). This installs a "pre-commit hook," or an action, that will run every time you attempt to commit.
```bash
pre-commit install
```
Now you can start integrating some [hooks](https://pre-commit.com/hooks.html) you want to use into a `.pre-commit-config.yaml` file that will executed before you commit. If you want contributors for your project, you should check out [pre-commit ci](https://pre-commit.ci/). This basically has the same functionality except that your contributors don't have to care about any of this stuff because it's all handled by the CI server. Check out its usage in this [simple project](https://github.com/hdadhich01/round-nutrition).

#### 🖊️ GPG
GPG is an encryption tool that comes packaged with Ubuntu. It can help you get verify your commits to ensure that every change comes from you. Also, it looks more professional when committing to reasonably sized community projects. You can set up a key to use on your machine by running the following.
```bash
echo "export GPG_TTY=$(tty)" >> ~/.zshrc
source ~/.zshrc
gpg --full-generate-key
```
Make sure you select `RSA and RSA`, `4096`, and `0` for the generation prompts. Specify your name and email address to match that of your GitHub account. Once generated, copy the key string through the following line.
```
gpg: key [COPY THIS] marked as ultimately trusted
```
Now you can run the following to add your key to `git` and enable commit signing through the command line.
```
git config --global user.signingkey [COPIED KEY]
git config --global commit.gpgsign true
```
To integrate this with source control in [VS Code](#️-visual-studio-code), turn on `Git: Enable Commit Signing` in `User` settings. Now, GitHub just needs a way to verify that it is actually you committing to a repository, which means you will give it the key you generated so it can check it against every commit's signature. Run the following command with your copied key.
```bash
gpg --armor --export [COPIED KEY]
```
Now save it to GitHub [here](https://github.com/settings/keys) by hitting `New GPG key` and pasting it into the `Key` field. The name can be set as `WSL (Ubuntu)`. Now when you attempt to commit, you will be prompted for the passphrase that you encrypted your key with. Once its through, you will see a green `Verified` box next to every single commit you make.

#### 🕛 WakaTime
Tracking how much time you are spending on your projects each day helps you develop a sense of priority and consistency. You can head over to [WakaTime](https://wakatime.com/) to set up an account.

As per the tools we used in this guide, you can set it up for [VS Code](https://wakatime.com/vs-code) and [zsh](https://wakatime.com/terminal). If you've got other editors, check out this [page](https://wakatime.com/plugins) to install their plugin. Their instructions are pretty straightforward.

## 🏁 Finish
Upgrade everything and force reboot your distribution.
```bash
sudo apt update && sudo apt upgrade
sudo reboot -f
```

### ❓ Errors
You might run into an error where you might have restarted your computer and open up your terminal to see the following layout, wondering where your original layout went. This only occurs with WSL2.
```
wslg [ ~ ]$
```
To fix this, open up a PowerShell terminal and run the following.
```pwsh
wsl --shutdown
wsl
```
Now you can relaunch your terminal session to restore your original layout.
