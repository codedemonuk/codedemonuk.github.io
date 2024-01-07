---
title: "Setting up SDKMAN! with Fish and Homebrew"
date: 2024-01-07 10:00
categories:
- Fish
- SDKMAN
- Homebrew
- macOS
---

Assuming you are a macOS user, managing your installed software with [HomeBrew][1] and using [Fish][2] as your shell of choice, these are the steps to allow you to use [SDKMAN][4] to manage your Java sdks for your projects

## Install SDKMAN with Homebrew

[SDKMAN][4] has it's own [HomeBrew Tap][3] which you can use to install the software.

```bash
brew tap SDKMAN/tap
brew install SDKMAN-cli
```

This will add the SDKMAN tap to your Homebrew configuration and then use it to install the SDKMAN CLI.

## Install Fisher

If you do not already have it installed, you will need to install [Fisher][5], this is a plug-in manager for the [Fish shell][2].

Full installation instructions are available in the [Readme on the Fisher project][6], but the crux of the installation is:

```bash
curl -sL https://raw.githubusercontent.com/jorgebucaran/fisher/main/functions/fisher.fish | source && fisher install jorgebucaran/fisher
```

## Install SDKMAN for Fish extension

You will need to install the [SDKMAN! for Fish extension][8].
This extension makes command `sdk` from [SDKMAN!][4] usable from fish, including auto-completion. Also adds binaries from installed SDKs to the PATH.

```bash
fisher install reitzig/SDKMAN-for-fish@v2.0.0
```

## Configure it all

At this point all the moving parts are installed, but some configuration still needs to be done to tie it all together.

Find out where SDKMAN! has been installed

```bash
echo $(brew --prefix SDKMAN-cli)/libexec
```

In my case, this told me that SDKMAN was installed to `/opt/homebrew/opt/SDKMAN-cli/libexec`
Keep a note of the result of that command as you will need it later.

You will need to configure the SDKMAN for Fish plugin to use SDKMAN from the custom location that Homebrew installed it into.

Create a configuration file for the SDKMAN plugin for fish.

```bash
touch ~/.config/fish/conf.d/config_sdk.fish
```

In that file, add the following command to tell the plugin where it can find SDKMAN

```bash
set -g __sdkman_custom_dir /opt/homebrew/opt/sdkman-cli/libexec
```

You should now have SDKMAN working and set up in the Fish shell.

[1]: https://brew.sh/
[2]: https://fishshell.com/
[3]: https://github.com/sdkman/homebrew-tap
[4]: https://sdkman.io/
[5]: https://github.com/jorgebucaran/fisher
[6]: https://github.com/jorgebucaran/fisher#readme
[8]: https://github.com/reitzig/sdkman-for-fish
