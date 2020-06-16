# macOS Pentest Setup
 A beginner's guide to setting up a pentest environment on macOS
 Inspired by [nicolahery](https://twitter.com/nicolas_hery)'s mac-dev-setup

- [System update](#system-update)
- [System preferences](#system-preferences)
- [Security](#security)
- [iTerm2](#iterm2)

## System update
First thing you need to do, on any OS actually, is update the system! For that: **Apple Icon > About This Mac** then **Software Update...**.

## System preferences
If this is a new computer, there are a couple of tweaks I like to make to the System Preferences. Feel free to follow these, or to ignore them, depending on your personal preferences.

In **Apple Icon > System Preferences**:
- Trackpad > Tap to click
- Keyboard > Key Repeat > Fast (all the way to the right)
- Keyboard > Delay Until Repeat > Short (all the way to the right)
- Dock > Automatically hide and show the Dock

## Security
I recommend checking that basic security settings are enabled.

In **Apple Icon > System Preferences**:
- Users & Groups: If you haven't already set a password for your user during the initial set up, you should do so now
- Security & Privacy > General: Require password immediately after sleep or screen saver begins
- Security & Privacy > FileVault: Make sure FileVault disk encryption is enabled

## iTerm2
### Install
Since we're going to be spending a lot of time in the command-line, let's install a better terminal than the default one. Download and install [iTerm2](http://www.iterm2.com/).

In **Finder**, drag and drop the **iTerm** Application file into the **Applications** folder.

You can now launch iTerm, through the **Launchpad** for instance.

Let's just quickly change some preferences. In **iTerm2 > Preferences...**, under the tab **General**, uncheck **Confirm closing multiple sessions** and **Confirm "Quit iTerm2 (Cmd+Q)" command** under the section **Closing**.

In the tab **Profiles**, create a new one with the "+" icon, and rename it. Then, select **Other Actions... > Set as Default**. Under the section **Window**, change the size to something better, like **Columns: 125** and **Rows: 35**.

When done, hit the red "X" in the upper left (saving is automatic in macOS preference panes). Close the window and open a new one to see the size change.
