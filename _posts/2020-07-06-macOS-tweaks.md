---
layout: post
title: Mac tweaks
subtitle: Some tweaks I like to do to my mac to change some default behaviours
show-avatar: false
tags: [macOS, tweaks]
---

macOS allows one to set a number of options that are unavailable in system preferences. It can often be hard to find a unified place for all the tweaks I like to make.

### App-by-app setting to close windows
I like to have apps reopen the windows that were open the last time I quit, this preference is in System Preferences, however there are some apps where I prefer they don't reopen the windows. This example will prevent Preview from reopening and can be set for pretty much any app, it works for all the latest versions of macOS including the Big Sur beta.

```
defaults write com.apple.Preview NSQuitAlwaysKeepsWindows -bool false
```

### Turn off volume HUD
Does what it says in the title.
From [here](https://apple.stackexchange.com/questions/16849/how-do-i-disable-the-volume-control-overlay)

```
sudo defaults write /System/Library/LaunchAgents/com.apple.OSDUIHelper Disabled -bool YES
```

### Hide desktop icons
Useful for conference calls or showing off your desktop in a screenshot. I also like using the desktop folder as a general inbox but without it creating visual clutter on my desktop. Just beware that clicking the desktop background will no longer count as switching to Finder so you will have to use the dock or app switcher to open the app.

```
defaults write com.apple.finder CreateDesktop -bool false && killall Finder
```

### Italics in terminal
The terminal emulator in macOS uses the xterm-256color profile by default which doesn't include support for italics, even if the terminal does.
To change the default create a file with the following content:

```shell
defaults write com.apple.Preview NSQuitAlwaysKeepsWindows -bool false
```

Then call this command: `tic <your-configuration-file>`

This will only affect the current user and will create a .terminfo folder in your home directory.

### Hosts file to block dodgy sites
The StevenBlack hosts file blocks a number of adware and malware domains, there are also versions blocking fake news, gambling, porn and social media in a variety of combinations. The below code will integrate the current version with your hosts file. As malware is being hosted in new places all the time it is advisable to update the hosts file from time to time, you might want to set up a launch daemon to do it automatically.

```shell
curl https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts | sudo tee -a /etc/hosts
egrep -ve "^#|^255.255.255.255|^127.|^0.|^::1|^ff..::|^fe80::" /etc/hosts | sort | uniq | egrep -e "[1,2]|::"
```

I also use [NextDNS](https://nextdns.io) which allows me to use encrypted DNS and keep track of my own queries as well as set rules block some sites from even being resolved.
