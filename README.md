# macOS Pentest Setup
 A beginner's guide to setting up a pentest environment on macOS<br>
 Inspired by [nicolahery](https://twitter.com/nicolas_hery)'s mac-dev-setup
<hr>

- [System update](#system-update)
- [System preferences](#system-preferences)
- [Security](#security)
- [iTerm2](#iterm2)
- [Homebrew](#homebrew)
- [Git](#git)
- [Visual Studio Code](#visual-studio-code)
- [Python](#python)

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

## Homebrew
Package managers make it so much easier to install and update applications (for Operating Systems) or libraries (for programming languages). The most popular one for macOS is [Homebrew](http://brew.sh/).

### Install
An important dependency before Homebrew can work is the **Command Line Developer Tools** for **Xcode**. These include compilers that will allow you to build things from source. You can install them directly from the terminal with:

```
xcode-select --install
```

Once that is done, we can install Homebrew by copy-pasting the installation command from the [Homebrew homepage](http://brew.sh/) inside the terminal after we read the source carefully 😉:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

Follow the steps on the screen. You will be prompted for your user password so Homebrew can set up the appropriate permissions.

Once installation is complete, you can run the following command to make sure everything works:

```
brew doctor
```

### Usage

To install a package (or **Formula** in Homebrew vocabulary) simply type:

```
brew install <formula>
```

To see if any of your packages need to be updated:

```
brew outdated
```

To update a package:

```
brew upgrade <formula>
```

Homebrew keeps older versions of packages installed, in case you want to rollback. That rarely is necessary, so you can do some cleanup to get rid of those old versions:

```
brew cleanup
```

To see what you have installed (with their version numbers):

```
brew list --versions
```

### Homebrew Services

A nice extension to Homebrew is [Homebrew Services](https://github.com/Homebrew/homebrew-services). It will automatically launch things like databases when your computer starts, so you don't have to do it manually every time.

Homebrew Services will automatically install itself the first time you run it, so there is nothing special to do.

After installing a service (for example a database), it should automatically add itself to Homebrew Services. If not, you can add it manually with:

```
brew services <formula>
```

Start a service with:

```
brew services start <formula>
```

At anytime you can view which services are running with:

```
brew services list
```

## Git
macOS comes with a pre-installed version of [Git](http://git-scm.com/), but we'll install our own through Homebrew to allow easy upgrades and not interfere with the system version. To do so, simply run:

```
brew install git
```

When done, to test that it installed fine you can run:

```
which git
```

The output should be `/usr/local/bin/git`.


On a Mac, it is important to remember to add `.DS_Store` (a hidden macOS system file that's put in folders) to your project `.gitignore` files. You also set up a global `.gitignore` file, located for instance in your home directory (but you'll want to make sure any collaborators also do it):

```
cd ~
curl -O https://raw.githubusercontent.com/avarx/mac-sec-setup/master/.gitignore
git config --global core.excludesfile ~/.gitignore
```

## Visual Studio Code
Go ahead and [download](https://code.visualstudio.com/Download) it. Open the **.dmg** file, drag-and-drop in the **Applications** folder, you know the drill now. Launch the application.

**Note**: At this point I'm going to create a shortcut on the macOS Dock for both for Visual Studio Code and iTerm. To do so, right-click on the running application and select **Options > Keep in Dock**.

Just like the terminal, let's configure our editor a little. Go to **Code > Preferences > Settings**. In the very top-right of the interface you should see an icon with brackets that appeared **{ }** (on hover, it should say "Open Settings (JSON)"). Click on it, and paste the following:

```json
{
  "editor.tabSize": 2,
  "editor.rulers": [80],
  "files.insertFinalNewline": true,
  "files.trimTrailingWhitespace": true,
  "workbench.editor.enablePreview": false
}
```

Feel free to tweak these to your preference. When done, save the file and close it.

Pasting the above JSON snippet was handy to quickly customize things, but for further setting changes feel free to search in the "Settings" panel that opened first (shortcut **Cmd+,**). When you're happy with your setup, you can save the JSON to quickly restore it on a new machine.

If you remember only one keyboard shortcut in VS Code, it should be **Cmd+Shift+P**. This opens the **Command Palette**, from which you can run pretty much anything.

Let's open the command palette now, and search for `Shell Command: Install 'code' command in PATH`. Hit enter when it shows up. This will install the command-line tool `code` to quickly open VS Code from the terminal. When in a projects directory, you'll be able to run:

```
cd myproject/
code .
```

VS Code is very extensible. To customize it further, open the **Extensions** tab on the left.

Let's do that now to customize the color of our editor. Search for the [Atom One Dark Theme](https://marketplace.visualstudio.com/items?itemName=akamud.vscode-theme-onedark) extension, select it and click **Install**. Repeat this for the [Atom One Light Theme](https://marketplace.visualstudio.com/items?itemName=akamud.vscode-theme-onelight).

Finally, activate the theme by going to **Code > Preferences > Color Theme** and selecting **Atom One Dark** (or **Atom One Light** if that is your preference).

## Python
macOS, like Linux, ships with [Python](http://python.org/) already installed. But you don't want to mess with the system Python (some system tools rely on it, etc.), so we'll install our own version using [pyenv](https://github.com/yyuu/pyenv). This will also allow us to manage multiple versions of Python (ex: 2.7 and 3) should we need to.

Install `pyenv` via Homebrew by running:

```
brew install pyenv
```

When finished, you should see instructions to add something to your profile. Open your `.bash_profile` in the home directory (you can use `code ~/.bash_profile`), and add the following line:

```bash
if command -v pyenv 1>/dev/null 2>&1; then eval "$(pyenv init -)"; fi
```

Save the file and reload it with:

```
source ~/.bash_profile
```

Before installing a new Python version, the [pyenv wiki](https://github.com/pyenv/pyenv/wiki) recommends having a few dependencies available:

```
brew install openssl readline sqlite3 xz zlib
```

We can now list all available Python versions by running:

```
pyenv install --list
```

Look for the latest 3.x version (or 2.7.x), and install it (replace the `.x.x` with actual numbers):

```
pyenv install 3.x.x
```

List the Python versions you have locally with:

```
pyenv versions
```

The star (`*`) should indicate we are still using the `system` version, which is the default. I recommend leaving it as the default as some [Node.js](https://nodejs.org/en/) packages will use it in their installation process.

You can switch your current terminal to another Python version with:

```
pyenv shell 3.x.x
```

You should now see that version when running:

```
python --version
```

In a project directory, you can use:

```
pyenv local 3.x.x
```

This will save that project's Python version to a `.python-version` file. Next time you enter the project's directory from a terminal, `pyenv` will automatically load that version for you.

For more information, see the [pyenv commands](https://github.com/yyuu/pyenv/blob/master/COMMANDS.md) documentation.

### pip

[pip](https://pip.pypa.io) was also installed by `pyenv`. It is the package manager for Python.

Here are a couple Pip commands to get you started. To install a Python package:

```
pip install <package>
```

To upgrade a package:

```
pip install --upgrade <package>
```

To see what's installed:

```
pip freeze
```

To uninstall a package:

```
pip uninstall <package>
```

### virtualenv

[virtualenv](https://virtualenv.pypa.io) is a tool that creates an isolated Python environment for each of your projects.

For a particular project, instead of installing required packages globally, it is best to install them in an isolated folder, that will be managed by `virtualenv`. The advantage is that different projects might require different versions of packages, and it would be hard to manage that if you install packages globally.

Instead of installing and using `virtualenv` directly, we'll use the dedicated `pyenv` plugin [pyenv-virtualenv](https://github.com/yyuu/pyenv-virtualenv) which will make things a bit easier for us. Install it via Homebrew:

```
brew install pyenv-virtualenv
```

After installation, add the following line to your `.bash_profile`:

```bash
if which pyenv-virtualenv-init > /dev/null; then eval "$(pyenv virtualenv-init -)"; fi
```

And reload it with:

```
source ~/.bash_profile
```

Now, let's say you have a project called `myproject`. You can set up a virtualenv for that project and the Python version it uses (replace `3.x.x` with the version you want):

```
pyenv virtualenv 3.x.x myproject
```

See the list of virtualenvs you created with:

```
pyenv virtualenvs
```

To use your project's virtualenv, you need to **activate** it first (in every terminal where you are working on your project):

```
pyenv activate myproject
```

If you run `pyenv virtualenvs` again, you should see a star (`*`) next to the active virtualenv.

Now when you install something:

```
pip install <package>
```

It will get installed in that virtualenv's folder, and not conflict with other projects.

You can also set your project's `.python-version` to point to a virtualenv you created:

```
pyenv local myproject
```

Next time you enter that project's directory, `pyenv` will automatically load the virtualenv for you.
