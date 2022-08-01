# Initial Data Science setup for Windows

I initially used to work on python and Data Science using MacOSX or Ubuntu, so changing to Windows was a confusing experience. Because of this I wrote a guide of everything I did for the initial setup of my computer to start programming.

This is how I set up a fresh windows PC to start working in machine learning and programming. I also keep this tutorial handy in case I do a clean OS install or if I need to check some of my initial settings.

My current Windows PC is using Windows 365.

<!-- MarkdownTOC autolink="true" autoanchor="true" -->

- [Basic Settings](#basic-settings)
    - [Install SublimeText](#install-sublimetext)
        - [Easy GitLab or GitHub math: Add paired $ signs to the keybinds](#easy-gitlab-or-github-math-add-paired--signs-to-the-keybinds)
    - [Easily transform 2 spaced indent to 4 spaced indent](#easily-transform-2-spaced-indent-to-4-spaced-indent)
- [Install Git Bash](#install-git-bash)
    - [Install zstd and rsync for Git Bash](#install-zstd-and-rsync-for-git-bash)
- [Setup Git for GitLab](#setup-git-for-gitlab)
    - [Check your branches in git log history in a pretty line](#check-your-branches-in-git-log-history-in-a-pretty-line)
    - [GitLab Markdown math expressions for README.md, etc.](#gitlab-markdown-math-expressions-for-readmemd-etc)
    - [GitHub Markdown math expressions for README.md, etc.](#github-markdown-math-expressions-for-readmemd-etc)
    - [Git remote origin for SSH](#git-remote-origin-for-ssh)
    - [Make a new Git \(LFS\) repository from local](#make-a-new-git-lfs-repository-from-local)
    - [Manage multiple GitHub or GitLab accounts](#manage-multiple-github-or-gitlab-accounts)
- [Install Python with pyenv-win and set it up](#install-python-with-pyenv-win-and-set-it-up)
    - [Install pyenv first](#install-pyenv-first)
        - [Option 1) Adding the paths to .bashrc so they're added each time Git Bash is opened](#option-1-adding-the-paths-to-bashrc-so-theyre-added-each-time-git-bash-is-opened)
        - [Option 2) Using Windows Settings](#option-2-using-windows-settings)
    - [Install and set up Python](#install-and-set-up-python)
    - [Read Python Command History between sessions](#read-python-command-history-between-sessions)
    - [How to upgrade Pyenv](#how-to-upgrade-pyenv)
    - [Install virtualenv](#install-virtualenv)
    - [Useful Data Science libraries](#useful-data-science-libraries)
- [Install and setup Flask for Python Web Development](#install-and-setup-flask-for-python-web-development)
- [Install and setup Ruby, Bundler and Jekyll for static websites](#install-and-setup-ruby-bundler-and-jekyll-for-static-websites)
- [Install LaTeX for documentation / reports](#install-latex-for-documentation--reports)
    - [Use my LaTeX helper shell scripts for faster compilation](#use-my-latex-helper-shell-scripts-for-faster-compilation)
    - [Run latex in git bash for version control](#run-latex-in-git-bash-for-version-control)
    - [Make LaTeX easier in Sublime Text:](#make-latex-easier-in-sublime-text)
- [Shell Scripting for convenience](#shell-scripting-for-convenience)
    - [Basic flag setup with getopts](#basic-flag-setup-with-getopts)
    - [Argparse-bash by nhoffman](#argparse-bash-by-nhoffman)
    - [LaTeX helpers](#latex-helpers)
- [Install Pandoc to convert/export markdown, HTML, LaTeX, Word](#install-pandoc-to-convertexport-markdown-html-latex-word)
- [Accessibility Stuff](#accessibility-stuff)
    - [Accessible Color Palettes with Paletton](#accessible-color-palettes-with-paletton)
    - [Reading tools for Neurodivergent people](#reading-tools-for-neurodivergent-people)
    - [Reading white PDFs](#reading-white-pdfs)
        - [Firefox](#firefox)
        - [Microsoft Edge](#microsoft-edge)
        - [Google Chrome](#google-chrome)

<!-- /MarkdownTOC -->

<a id="basic-settings"></a>
## Basic Settings

There are some basic things you should do to make programming in Windows easier.

- Setup the initial WiFi connection.
- When leaving the desk always press WIN+L to lock under password.
- For ease of use, make hidden files and file extensions visible.
    - Open an explorer window, under View > Show > File name extensions, Hidden items

<a id="install-sublimetext"></a>
### Install SublimeText

- Install SublimeText4 for ease of use (this is my personal favorite, but it's not necessary)

https://www.sublimetext.com/download

- Paste the SublimeText4 preferences (my personal preferences)

```
{
    "ignored_packages":
    [
        "Vintage",
    ],
    "spell_check": true,
    "tab_size": 4,
    "translate_tabs_to_spaces": true,
    "copy_with_empty_selection": false
}
```

For the moment, there's no equivalent to `sudo` that I know of, so we skip the root password setup as well.

Also, Sublime Text is all about the plugins. Install Package Control by typing CTRL+Shift+P, then typing "Install Package Control"

Then here's some cool packages to try:

- [LaTeXTools](https://packagecontrol.io/packages/LaTeXTools)
- [MarkdownTOC](https://packagecontrol.io/packages/MarkdownTOC)
- [MarkdownPreview](https://packagecontrol.io/packages/MarkdownPreview)
- [MarkdownEditing](https://packagecontrol.io/packages/MarkdownEditing)
- [IncrementSelection](https://packagecontrol.io/packages/Increment%20Selection)

In MarkdownTOC.sublime-settings, paste the following for hyperlink markdowns and compatibility with MarkdownPreview:

```
{
  "defaults": {
    "autoanchor": true,
    "autolink": true,
    "markdown_preview": "github",
    "uri_encoding": false
  },
}
```

<a id="easy-gitlab-or-github-math-add-paired--signs-to-the-keybinds"></a>
#### Easy GitLab or GitHub math: Add paired $ signs to the keybinds

I found myself needing paired $dollar signs$ for math expressions in either LaTeX, GitLab with KeTeX or GitHub also with a different syntax but still some interpretation of TeX.

Searching for [how to do it on macros](https://forum.sublimetext.com/t/snippet-wrap-current-line-or-selection/53285), I found this post about keybindings which is a way better solution:

https://stackoverflow.com/questions/34115090/sublime-text-2-trying-to-escape-the-dollar-sign

Which, as long as we implement the double escaped dollar sign solution, we can use freely.

- Preferences > Key Bindings:
- Add this inside the brackets:
```
// Auto-pair dollar signs
{ "keys": ["$"], "command": "insert_snippet", "args": {"contents": "\\$$0\\$"}, "context":
    [
        { "key": "setting.auto_match_enabled", "operator": "equal", "operand": true },
        { "key": "selection_empty", "operator": "equal", "operand": true, "match_all": true },
        { "key": "following_text", "operator": "regex_contains", "operand": "^(?:\t| |\\)|]|\\}|>|$)", "match_all": true },
        { "key": "preceding_text", "operator": "not_regex_contains", "operand": "[\\$a-zA-Z0-9_]$", "match_all": true },
        { "key": "eol_selector", "operator": "not_equal", "operand": "string.quoted.double", "match_all": true }
    ]
},
{ "keys": ["$"], "command": "insert_snippet", "args": {"contents": "\\$${0:$SELECTION}\\$"}, "context":
    [
        { "key": "setting.auto_match_enabled", "operator": "equal", "operand": true },
        { "key": "selection_empty", "operator": "equal", "operand": false, "match_all": true }
    ]
},
{ "keys": ["$"], "command": "move", "args": {"by": "characters", "forward": true}, "context":
    [
        { "key": "setting.auto_match_enabled", "operator": "equal", "operand": true },
        { "key": "selection_empty", "operator": "equal", "operand": true, "match_all": true },
        { "key": "following_text", "operator": "regex_contains", "operand": "^\\$", "match_all": true }
    ]
},
{ "keys": ["backspace"], "command": "run_macro_file", "args": {"file": "Packages/Default/Delete Left Right.sublime-macro"}, "context":
    [
        { "key": "setting.auto_match_enabled", "operator": "equal", "operand": true },
        { "key": "selection_empty", "operator": "equal", "operand": true, "match_all": true },
        { "key": "preceding_text", "operator": "regex_contains", "operand": "\\$$", "match_all": true },
        { "key": "following_text", "operator": "regex_contains", "operand": "^\\$", "match_all": true }
    ]
},
```

<a id="easily-transform-2-spaced-indent-to-4-spaced-indent"></a>
### Easily transform 2 spaced indent to 4 spaced indent

https://forum.sublimetext.com/t/can-i-easily-change-all-existing-2-space-indents-to-4-space-indents/40158/2

- Sublime text, lower right corner
- Click on Spaces
- Select the current space number
- Click Convert indentation to Tabs
- Select the desired space number
- Click Convert indentation to Spaces

<a id="install-git-bash"></a>
## Install Git Bash

I followed this guide for using git on Windows:<br>
https://www.pluralsight.com/guides/using-git-and-github-on-windows

Download and Install from: <br>
https://git-scm.com/download/win

I used most of the suggestions on installation, except for a few exceptions. Here's the options I chose:

- Check all the check-marks at the beginning to have right click menus for GitBash and shortcuts in the Windows pane.
- Make sure to install GitLFS along with the installation.
- Associate `.sh` and `.git` files with GitBash
- Use **Nano** editor as default
- Override the `master` branch to `main`
- When prompted to the **Adjusting your PATH environment window** : choose **Use Git from Git Bash only**
- Use Bundled OpenSSH
- Use OpenSSL
- When choosing line-endings: **Checkout as-is, commit Unix-style line endings**
- Use MinTTY
- Choose the default behavior of `git pull` as `fast-forward only`
- Use Git credential manager
- Enable file system caching
- No experimental tools with known bugs.

Now click **Install** and wait for the installation to finish.

One thing I noticed is that if I open the GitBash software from the Windows pane, windows command prompt `cmd` style commands such as `cls` will run, while if I right click a folder and run GitBash from that location, pseudo-Unix style commands such as `clear` will run. It is confusing and I'm used to Unix style commands so remember to always right click open GitBash.

<a id="install-zstd-and-rsync-for-git-bash"></a>
### Install zstd and rsync for Git Bash

Installing rsync is necessary to sync files with a Linux server from a windows machine, which is useful to run big programs like machine learning when that server has a powerful GPU. However, rsync is a Unix command so we have to install it manually to be able to use it with Git Bash.

https://shchae7.medium.com/how-to-use-rsync-on-git-bash-6c6bba6a03ca

1. Open Git Bash as administrator

2. Install zstd

```
mkdir zstd
cd zstd
curl -L -O https://github.com/facebook/zstd/releases/download/v1.4.4/zstd-v1.4.4-win64.zip
unzip zstd-v1.4.4-win64.zip
echo "alias zstd='~/zstd/zstd.exe'" >> ~/.bashrc
source ~/.bashrc
```

3. Get rsync.exe

```
cd
mkdir rsync
cd rsync
curl -L -O https://repo.msys2.org/msys/x86_64/rsync-3.2.3-1-x86_64.pkg.tar.zst
zstd -d rsync-3.2.3–1-x86_64.pkg.tar.zst
tar -xvf rsync-3.2.3-1-x86_64.pkg.tar
cp ./usr/bin/rsync.exe /usr/bin
```

4. Install dependencies

```
cd
mkdir libzstd
cd libzstd
curl -L -O https://repo.msys2.org/msys/x86_64/libzstd-1.4.8-1-x86_64.pkg.tar.zst
zstd -d libzstd-1.4.8-1-x86_64.pkg.tar.zst
tar -xvf libzstd-1.4.8-1-x86_64.pkg.tar
cp ./usr/bin/msys-zstd-1.dll /usr/bin
```

```
cd
mkdir libxxhash
cd libxxhash
curl -L -O https://repo.msys2.org/msys/x86_64/libxxhash-0.8.0-1-x86_64.pkg.tar.zst
zstd -d libxxhash-0.8.0-1-x86_64.pkg.tar.zst
tar -xvf libxxhash-0.8.0-1-x86_64.pkg.tar
cp ./usr/bin/msys-xxhash-0.8.0.dll /usr/bin
```

5. Check if rsync is working

On a normal git bash session:

```
rsync
```

It should output the different options you can use with it.

<a id="setup-git-for-gitlab"></a>
## Setup Git for GitLab

At first, we need to make sure of the path that `.gitconfig` will be saved by default so let's config the user and email through GitBash itself.

Run these commands and change in your username and email where appropriate.
```
git config --global user.name "Your_GitLab_username"
git config --global user.email "your_email@company.com"
```

Next, Git on Windows has a limitation on filenames compared to Linux or MacOSX. Here's an explanation found [here](https://stackoverflow.com/a/22575737)

> Git has a limit of 4096 characters for a filename, except on Windows when Git is compiled with msys. It uses an older version of the Windows API and there's a limit of 260 characters for a filename. <br><br>
So as far as I understand this, it's a limitation of msys and not of Git. You can read the details here: https://github.com/msysgit/git/pull/110 <br><br>
You can circumvent this by using another Git client on Windows or set core.longpaths to true as explained in other answers.<br><br> 
`git config --system core.longpaths true` <br><br>
Git is build as a combination of scripts and compiled code. With the above change some of the scripts might fail. That's the reason for core.longpaths not to be enabled by default. <br><br> 
The windows documentation at https://docs.microsoft.com/en-us/windows/win32/fileio/maximum-file-path-limitation?tabs=cmd#enable-long-paths-in-windows-10-version-1607-and-later has some more information: <br><br>
>>   Starting in Windows 10, version 1607, MAX_PATH limitations have been removed from common Win32 file and directory functions. However, you must opt-in to the new behavior. <br><br> A registry key allows you to enable or disable the new long path behavior. To enable long path behavior set the registry key at HKLM\SYSTEM\CurrentControlSet\Control\FileSystem LongPathsEnabled (Type: REG_DWORD)

Since we don't want to mess up the system settings, let's set it up with global config files for now:

```
git config --global core.longpaths true
```

Now we can see that the `.gitconfig` file is under `"C:\Users\<user>\.gitconfig"`. I can now open that on SublimeText and paste my favorite settings for git:

```
# ~/.gitconfig

[user]
    name = YOUR_USERNAME
    email = YOUR_EMAIL
[color]
    ui = auto
[merge]
    conflictstyle = diff3
[core]
    editor = nano
    autocrlf = input
    fileMode = false
    longpaths = true
[pull]
    ff = only
[alias]
    adog = log --all --decorate --oneline --graph
```

That last one, `git adog` is very useful as I explain below:

<a id="check-your-branches-in-git-log-history-in-a-pretty-line"></a>
### Check your branches in git log history in a pretty line

This makes your history tree pretty and easy to understand inside of the terminal.
I found this in [https://stackoverflow.com/a/35075021](https://stackoverflow.com/a/35075021)

```
git log --all --decorate --oneline --graph
```

Not everyone would be doing a git log all the time, but when you need it just remember: 
"A Dog" = git log --all --decorate --oneline --graph

Actually, let's set an alias:

```
git config --global alias.adog "log --all --decorate --oneline --graph"
```

This adds the following to the .gitconfig file:

```
[alias]
        adog = log --all --decorate --oneline --graph
```

And you run it like:

```
git adog
```

<a id="gitlab-markdown-math-expressions-for-readmemd-etc"></a>
### GitLab Markdown math expressions for README.md, etc.

Following this guide, math is different in GitLab markdown than say, GitHub or LaTeX.
However, inside of the delimiters, it renders it using KaTeX, which uses LaTeX math syntax! 

https://docs.gitlab.com/ee/user/markdown.html#math

Inline: 
```
> $`a^2 + b^2 = c^2`$
```

Renders as: $`a^2 + b^2 = c^2`$

Block:
```
> ```math
> a^2 + b^2 = c^2
> ```
```

Renders as:

```math
a^2 + b^2 = c^2
```

But it only supports one line of math, so for multiple lines you have to do this:

```
> ```math
> a^2 + b^2 = c^2
> ```
> ```math
> c = \sqrt{ a^2 + b^2 }
> ```
```

Renders as:

```math
a^2 + b^2 = c^2
```
```math
c = \sqrt{ a^2 + b^2 }
```

It can even display matrices and the like:

```
> ```math
> l_1 = 
> \begin{bmatrix}
>     \begin{bmatrix}
>         x_1 & y_1
>     \end{bmatrix} \\
>     \begin{bmatrix}
>         x_2 & y_2
>     \end{bmatrix} \\
>     ... \\
>     \begin{bmatrix}
>         x_n & y_n
>     \end{bmatrix} \\
> \end{bmatrix}
> ```
```

```math
l_1 = 
\begin{bmatrix}
    \begin{bmatrix}
        x_1 & y_1
    \end{bmatrix} \\
    \begin{bmatrix}
        x_2 & y_2
    \end{bmatrix} \\
    ... \\
    \begin{bmatrix}
        x_n & y_n
    \end{bmatrix} \\
\end{bmatrix}
```

However, % comments will break the environment.

Math syntax in LaTeX:

https://katex.org/docs/supported.html

<a id="github-markdown-math-expressions-for-readmemd-etc"></a>
### GitHub Markdown math expressions for README.md, etc.

Following this guide, math is different in GitLab markdown than say, GitHub or LaTeX.
However, inside of the delimiters, it renders it using KaTeX, which uses LaTeX math syntax! 

https://docs.gitlab.com/ee/user/markdown.html#math

Inline: 
```
> $a^2 + b^2 = c^2$
```

Renders as: $a^2 + b^2 = c^2$

Block:
```
> $$a^2 + b^2 = c^2$$
```

Renders as:

$$a^2 + b^2 = c^2$$

But it only supports one line of math, so for multiple lines you have to do this:

```
> $$a^2 + b^2 = c^2$$
> <!-- (line break is important) -->
> $$c = \sqrt{ a^2 + b^2 }$$
```

Renders as:

$$a^2 + b^2 = c^2$$

$$c = \sqrt{ a^2 + b^2 }$$

It can even display matrices and the like:

```
> $$
> l_1 = 
> \begin{bmatrix}
>     \begin{bmatrix}
>         x_1 & y_1
>     \end{bmatrix} \\
>     \begin{bmatrix}
>         x_2 & y_2
>     \end{bmatrix} \\
>     ... \\
>     \begin{bmatrix}
>         x_n & y_n
>     \end{bmatrix} \\
> \end{bmatrix}
> $$
```

$$
l_1 = 
\begin{bmatrix}
    \begin{bmatrix}
        x_1 & y_1
    \end{bmatrix} \\
    \begin{bmatrix}
        x_2 & y_2
    \end{bmatrix} \\
    ... \\
    \begin{bmatrix}
        x_n & y_n
    \end{bmatrix} \\
\end{bmatrix}
$$


However, % comments will break the environment.

Math syntax in LaTeX:

https://katex.org/docs/supported.html


<a id="git-remote-origin-for-ssh"></a>
### Git remote origin for SSH

With SSH the structure would be this:
```
git clone ssh://git@<HOST>:<PORT>/username/your-project.git
```

**Create a new repository**

```
git clone http://<HOST>:<PORT>/username/your-project.git
cd your-project
touch README.md
git add README.md
git commit -m "add README"
git push -u origin master
```

**Existing folder**

```
cd existing_folder
git init
git remote add origin http://<HOST>:<PORT>/username/your-project.git
git add .
git commit -m "Initial commit"
git push -u origin master
```

**Existing Git repository**

```
cd existing_repo
git remote rename origin old-origin
git remote add origin http://<HOST>:<PORT>/username/your-project.git
git push -u origin --all
git push -u origin --tags
```

To change from SSH to HTTP:
```
git remote set-url origin http://<HOST>:<PORT>/username/your-project.git
```

<a id="make-a-new-git-lfs-repository-from-local"></a>
### Make a new Git (LFS) repository from local

Now that we have Git and Python installed, we can make our first project. I like to leave this part of the tutorial in even if it doesn't classify as a setup because using Git and GitLFS was confusing at first.

First make a repository on GitHub with no .gitignore, no README and no license.
Then, on local terminal, cd to the directory of your project and initialize git
```
cd path/to/your/project
git init
```

If using Git LFS:
```
git lfs install
```

Make a .gitignore depending on which files you don't want in the repository and add it
```
git add .gitignore
```

If using Git LFS, add the tracking settings for this project (For example, heavy csv files in this case)
```
git lfs track "*.csv"
```

And then add them to git
```
git add .gitattributes
```

Commit these changes first
```
git commit -m "First commit, add .gitignore and .gitattributes"
```

Now add all the data from your local repository. `git add .` adds all the files in the folder.
```
git add .
```

Depending on the size of your project, it might be wiser to add it in parts instead of all at once. e.g.
```
git add *.py
git add *.csv
...
```
or
```
git add dir1
git add dir2
...
```

Check if all the paths are added
```
git status
```

Check if all the Git LFS files are tracked correctly
```
git lfs ls-files
```

If so, commit.
```
git commit -m "First data commit"
```

Set the new remote URL from the repository you created on GitHub. It'll appear with a copy button and everything, and end in .git
```
git remote add origin remote_repository_URL_here
```

Verify the new remote URL
```
git remote -v
```

Set upstream and then push only the lfs files to remote
```
git lfs push origin master
```

Afterwards push normally to upload everything
```
git push --set-upstream origin master
```

You only need to write --set-upstream origin master the first time for normal `push`, after this just write push. For git lfs you always have to write it.

<a id="manage-multiple-github-or-gitlab-accounts"></a>
### Manage multiple GitHub or GitLab accounts

Because I want to update my personal code when I find better ways to program at work, I want to push and pull from my personal GitHub account aside from the work GitLab projects. **CAUTION: DON'T UPLOAD COMPANY SECRETS TO YOUR PERSONAL ACCOUNT**

To be able to do this, I followed these guides:<br>
https://blog.gitguardian.com/8-easy-steps-to-set-up-multiple-git-accounts/


https://medium.com/the-andela-way/a-practical-guide-to-managing-multiple-github-accounts-8e7970c8fd46


1. Generate an SSH key
First, create an SSH key for your personal account:
```
ssh-keygen -t rsa -b 4096 -C "your_personal_email@example.com" -f ~/.ssh/<personal_key> 
```
Then for your work account:
```
ssh-keygen -t rsa -b 4096 -C "your_work_email@company.com" -f ~/.ssh/<work_key> 
```

2. Add a passphrase

Then add a passphrase and press enter, it will ask for it twice. Press enter again.

To update the passphrase for your SSH keys:

```
ssh-keygen -p -f ~/.ssh/<personal_key>
```

You can check your newly created key with:

```
ls -la ~/.ssh
```

which should output <personal_key> and <personal_key>.pub.

Do the same steps for the <work_key>.

3. Tell ssh-agent

The website has an -K tag that works for macOSX and such but we don't need it.

```
eval "$(ssh-agent -s)" && \
ssh-add ~/.ssh/<personal_key> 
ssh-add ~/.ssh/<work_key> 
```

4. Edit your SSH config

```
nano ~/.ssh/config
-----------nano----------
# Work account - default
Host <some_host_name_work>
  HostName <HOST>:<PORT>
  User git
  IdentityFile ~/.ssh/<work_key> 

# Personal account
Host <personal_host_name>
  HostName github.com
  User git
  IdentityFile ~/.ssh/<personal_key>

CTRL+O
CTRL+X
-------------------------
```

5. Copy the SSH public key

```
cat ~/.ssh/<personal_key>.pub | clip
```

Then paste on your respective website settings, such as the GitHub SSH settings page. Title it something you'll know it's your work computer.

Same for your <work_key>

6. Structure your workspace for different profiles

Now, for each key pair (aka profile or account), we will create a .conf file to make sure that your individual repositories have the user settings overridden accordingly.
Let’s suppose your home directory is like that:

```
/myhome/
    |__.gitconfig
    |__work/
    |__personal/
```

We are going to create two overriding .gitconfigs for each dir like this:

```
/myhome/
|__.gitconfig
|__work/
     |_.gitconfig.work
|__personal/
    |_.gitconfig.pers
```

Of course the folder and filenames can be whatever you prefer.

7. Set up your Git configs

In the personal git projects folder, make `.gitconfig.pers`

```
nano ~/personal/.gitconfig.pers
---------------nano-----------------
# ~/personal/.gitconfig.pers
 
[user]
email = your_personal_email@example.com
name = Your Name
 
[github] #or gitlab or whatever
user = "personal-username"
 
[core]
sshCommand = “ssh -i ~/.ssh/<personal_key>”

```


```

# ~/work/.gitconfig.work
 
[user]
email = your_work_email@company.com
name = Your Name
 
[github] #or gitlab or whatever
user = "work_username"

[core]
sshCommand = “ssh -i ~/.ssh/<work_key>”


```

And finally add this to the end of your original main `.gitconfig` file:

```
[includeIf “gitdir:~/personal/”] # include for all .git projects under personal/ 
path = ~/personal/.gitconfig.pers
 
[includeIf “gitdir:~/work/”]
path = ~/work/.gitconfig.work
```

Now finally to confirm if it worked, go to any work project you have and type the following:

```
cd ~/work/work-project
git config user.email
```

It should be your work e-mail.

Now go to a personal project:

```
cd ~/personal/personal-project
git config user.email
```

And it should output your personal e-mail.

To clone new projects, specially private or protected ones, use the username before the website:

```
git clone https://<username>@github.com/<organization>/<repo>.git
```

And done! When you push or pull from the personal account you might encounter some 2 factor authorizations at login, but otherwise it's ready to work on both personal and work projects.

<a id="install-python-with-pyenv-win-and-set-it-up"></a>
## Install Python with pyenv-win and set it up

A lot of tutorials use Anaconda but I will use Python by itself and virtualenv for extreme cases.

<a id="install-pyenv-first"></a>
### Install pyenv first

First let's install pyenv-win, which is a fork of pyenv specifically for installing windows versions of python. The benefit of this is it lets you install several versions of python at the same time and use different ones in different projects, without path conflicts.

Let's follow the installation guide here:<br>
https://github.com/pyenv-win/pyenv-win#installation

```
git clone https://github.com/pyenv-win/pyenv-win.git "$HOME/.pyenv"
```

The next step is to add the pyenv paths to the PATH environmental variable so the git bash reads them correctly.

There is two ways of doing this, but I chose option 1 because it's faster and can be copied to new machines.

<a id="option-1-adding-the-paths-to-bashrc-so-theyre-added-each-time-git-bash-is-opened"></a>
#### Option 1) Adding the paths to .bashrc so they're added each time Git Bash is opened

```
nano ~/.bashrc
---- add in nano interface---
# PYENV paths
export PATH=$PATH:~/.pyenv/pyenv-win/bin:~/.pyenv/pyenv-win/shims
export PYENV=~/.pyenv/pyenv-win/
export PYENV_ROOT=~/.pyenv/pyenv-win/
export PYENV_HOME=~/.pyenv/pyenv-win/
export PYENV_PYTHON_EXE=$(dirname $(pyenv.bat which python))
export PATH=$PATH:$PYENV_PYTHON_EXE
# To update PYENV_PYTHON_EXE if pyenv changes versions close bash and open again
CTRL+O
CTRL+X
--------------------
source ~/.bashrc
```

<a id="option-2-using-windows-settings"></a>
#### Option 2) Using Windows Settings 

Go to System Properties, search for Environmental Variables and click the Environmental Variables button that results from an old fashioned settings window.
Under User Environmental Variables add a NEW:

```
Variable name = PYENV
Variable value= %USERPROFILE%\.pyenv\pyenv-win\
```
```
Variable name = PYENV_ROOT
Variable value= %USERPROFILE%\.pyenv\pyenv-win\
```
```
Variable name = PYENV_HOME
Variable value= %USERPROFILE%\.pyenv\pyenv-win\
```

Go to the User Environmental Variables again and select the Path variable, click Edit:

In the edit window, add:
```
%USERPROFILE%\.pyenv\pyenv-win\bin
%USERPROFILE%\.pyenv\pyenv-win\shims
```

Click OK until all the windows go away.

<a id="install-and-set-up-python"></a>
### Install and set up Python

**Restart Git Bash**

```
echo $PYENV
echo $PATH
```

And the new environmental variables should be added.

Now in Git Bash check if it works

```
pyenv --version
```

<!-- Now we already have a version of Python installed, but that is not the Pyenv dependent python.

```
$ which python
/c/Program Files/Python310/python
$ python -V
Python 3.10.4
``` -->

Let's install python 3.9.6 since that's the latest under pyenv-win (`pyenv install -l` to check).

```
pyenv install 3.9.6
pyenv global 3.9.6
```

That sets 3.9.6 as the default.

Go to System Properties, search for Environmental Variables and click the Environmental Variables button that results from an old fashioned settings window.

From the User Path variable: delete `%USERPROFILE%\AppData\Local\Microsoft\WindowsApps`, which is conflicting with the `python` command for some reason.

Click OK until all the windows go away.

**Restart Git Bash**

```
which python
    >>/c/Users/USERNAME/.pyenv/pyenv-win/shims/python
where python
    >>C:\Users\USERNAME\.pyenv\pyenv-win\shims\python
    >>C:\Users\USERNAME\.pyenv\pyenv-win\shims\python.bat
python --version
    >>Python 3.9.6
which pip
    >>/c/Users/USERNAME/.pyenv/pyenv-win/shims/pip
where pip
    >>C:\Users\USERNAME\.pyenv\pyenv-win\shims\pip
    >>C:\Users\USERNAME\.pyenv\pyenv-win\shims\pip.bat
pip --version
    >>pip 22.0.4 from c:\users\USERNAME\.pyenv\pyenv-win\versions\3.9.6\lib\site-packages\pip (python 3.9)
```

All these should now return pyenv versions.

Now if we just run `python` in Git Bash, it will hang instead of opening the interpreter. In order to run Python in Git Bash the same as we did in Unix based systems, we have to go back to the `.bashrc` and add a path to the a new alias.

```
nano ~/.bashrc
----nano interface---
# To run Python in Git Bash like in Unix
alias python='winpty python.exe'
CTRL+O
CTRL+X
source ~/.bashrc
--------------------
```

\* Solution gotten from:<br>
https://qiita.com/birdwatcher/items/acbc79005d24616de5b6

Now typing `python` in Git Bash should open the python interface without hanging.

Let's also upgrade pip:
```
pip install --upgrade pip
```

<a id="read-python-command-history-between-sessions"></a>
### Read Python Command History between sessions

There's a way to make life easier and keep the python history between sessions.

```
pip install pyreadline
```

However, this has issues with non-ASCII characters and the library isn't being updated, so we'll go to the source files and edit the code a little:

Go to `~/.pyenv/pyenv-win/versions/3.9.6/lib/site-packages/pyreadline/lineeditor/history.py`

And edit like shown in this website:<br>
https://programmerah.com/error-when-starting-python-in-windows-38032/

```
def read_history_file(self, filename=None): 
        '''Load a readline history file.'''
        if filename is None:
            filename = self.history_filename
        try:
            #for line in open(filename, 'r'): #previously was like this
            for line in open(filename, 'r', encoding='utf-8'): #correct to this
                self.add_history(lineobj.ReadLineTextBuffer(ensure_unicode(line.rstrip())))
        except IOError:
            self.history = []
            self.history_cursor = 0
```

Then restart the Git-Bash and it should be working for all sorts of texts!

<a id="how-to-upgrade-pyenv"></a>
### How to upgrade Pyenv

If installed via Git go to `%USERPROFILE%\.pyenv\pyenv-win` (which is your installed path) and run `git pull`.

<a id="install-virtualenv"></a>
### Install virtualenv

Virtualenv allows me to install different libraries under pip for specific projects.

```
pip install virtualenv
```

Usage guide is here:<br>
https://mothergeo-py.readthedocs.io/en/latest/development/how-to/venv-win.html

<a id="useful-data-science-libraries"></a>
### Useful Data Science libraries

This is my generic fresh start install so I can work. There's more libraries with complicated installations in other repositories of mine, and you might not wanna run this particular piece of code without checking what I'm doing first. For example, you might have a specific version of Tensorflow that you want, or some of these you won't use. But I'll leave it here as reference.

```
pip install numpy scipy statsmodels matplotlib \
sklearn beautifulsoup4 requests selenium gensim \
nltk langdetect sympy pyclustering \
tensorflow tflearn keras minepy
```

Although some of these (specifically minepy) need the Visual Studio C++ Build Tools as a dependency, so install it first:<br>
https://visualstudio.microsoft.com/visual-cpp-build-tools/

```
pip install minepy
```

And some more python libraries that will be useful for regular tasks:

```
pip install more_itertools pandas pathlib tqdm retry
```

<a id="install-and-setup-flask-for-python-web-development"></a>
## Install and setup Flask for Python Web Development

I'm using this guide:
https://flask.palletsprojects.com/en/2.1.x/installation/#install-flask

For Web Development, it's apparently better to make a Virtual Environment to install flask project-wise instead of system or user level.

First we go to our project and make the virtual environment.

```
cd my-project
python -m venv venv
. venv/scripts/activate
```
it might also be
```
. venv/bin/activate
```
so if one fails try the other.

Activate results in the python and pip versions to be internal to the project now and active in the bash:

```
which python
>>> .... my-project\venv/Scripts/python

pip --version
pip 22.1 from c:\users\...\my-project\venv\lib\site-packages\pip (python 3.9)
```

So since this pip is empty, let's install ONLY what we need for the project:

```
pip install --upgrade pip
pip install selenium beautifulsoup4 pandas pathlib retry
pip install flask
```

Now let's test it:

I'm using this guide here:

https://flask.palletsprojects.com/en/2.1.x/quickstart/

Under: `my-project/python/hello.py`
```
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"
```
Then in bash:

```
cd my-project/python
export FLASK_APP=hello
flask run
```
and it should return:

```
 * Serving Flask app 'hello' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://127.0.0.1:5000 (Press CTRL+C to quit)
```

Unlike Jekyll, it won't update as you edit, unless you set up a development environment variable:

```
export FLASK_APP=hello
export FLASK_ENV=development
flask run
```

It will update, but you still have to click refresh on the screen.

```
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<h1>Hello, World!</h1>"
```

Now to make the project a package and keep running under the same structure as before, now I use this structure: (which by the way you can output with `tree /F /A | clip` on the CMD, or with `tree.com //f //a | clip` on Git Bash)

```
my-project
|   .gitignore
|   README.md
|   requirements.txt
|   
+---logs
|       tasklog.md
|       
+---python
|   |   ProjectPaths.py
|   |   
|   +---package
|   |   |   module.py
|   |   |   __init__.py
|   |   |   
|   |   \---__pycache__
|   |           
|   +---tests
|   |   |   0_test.py
|   |   |   
|   |   \---__pycache__
|   |           
|   \---__pycache__
|           
\---venv
```

`ProjectPaths.py` is just a bunch of methods I like to call to make directories without much hassle.

To run the tests and the files in the package, now the command is like this:

```
cd my-project/python
python -m tests.0_test
```

Notice that it's a `.` instead of a `/` and also there's no `.py`
It should now run and import as if from the parent directory `python`


<a id="install-and-setup-ruby-bundler-and-jekyll-for-static-websites"></a>
## Install and setup Ruby, Bundler and Jekyll for static websites

Sometimes it might be necessary to present results in HTML websites.
For this, I like to use Jekyll, which needs Ruby and Bundler. First lets install all our dependencies, following this guide:<br>
https://jekyllrb.com/docs/installation/windows/

Install Ruby+Devkit on Windows with [RubyInstaller](https://rubyinstaller.org/)

- Don't forget to select the add Ruby related items to PATH option
- Run the ridk install at the last stage of the installation wizard.
- You'll be prompted to install MSYS2, I selected option 3.

Open a new command prompt window from the start menu, so that changes to the PATH environment variable becomes effective. 
`echo %PATH%` on cmd and `echo $PATH` on Git Bash should both have Ruby related paths now.


You can do this on the Git Bash too, but the output will be delayed, so run on cmd.

Install Jekyll and Bundler using `gem install jekyll jekyll-sitemap bundler`

Check if installed properly `jekyll -v` on cmd or git bash.

Now it's installed! I'll be using this for local websites, but we're going to follow a tutorial on how to make Jekyll Github Pages, so even though we're not using GitHub, give this a read.

https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll

Make a new repository for your website on local git.

Now, once you have your webiste repository and you're ready to test the jekyll serve, do the following:

```
cd (your_repository_here)
bundle init
bundle add jekyll
bundle add jekyll-sitemap
bundle add webrick
```

And then all that's left to do is to serve the website with jekyll!
Also for the sitemaps make sure to check this tutorial:

https://github.com/jekyll/jekyll-sitemap

And add this to your `_config.yml`
```
url: "https://example.com" # the base hostname & protocol for your site
plugins:
  - jekyll-sitemap
```

```
bundle exec jekyll serve
```

If you get an error like:
```
Could not find webrick-1.7.0 in any of the sources
Run `bundle install` to install missing gems.
```

Do as it says and just run:
```
bundle install
```

Now you can work on the website and look at how it changes on screen.


<a id="install-latex-for-documentation--reports"></a>
## Install LaTeX for documentation / reports

https://www.latex-project.org/

Because I'm used to Unix systems already, the most usable packaging that offers that similarity across systems seems to be TeXLive.

https://tug.org/texlive/windows.html

Download the installer and run:

https://mirror.ctan.org/systems/texlive/tlnet/install-tl-windows.exe

Make sure default paper is A4.

Now after installation you might get some install failures for a few packages, and will get a command with `tlmgr` and some options to run. That command can only be run in the CMD prompt and not in Git Bash.

<a id="use-my-latex-helper-shell-scripts-for-faster-compilation"></a>
### Use my LaTeX helper shell scripts for faster compilation

https://github.com/elisa-aleman/latex_helpers

I made these shell scripts to help in compiling faster when using bibliographies and to delete cumbersome files when not necessary every time I compile. Since they are .sh scripts, they run normally with git bash.

<a id="run-latex-in-git-bash-for-version-control"></a>
### Run latex in git bash for version control

If you need to configure Tex Live using `tlmgr`, it's necessary to run the commands in the CMD prompt. However, `pdflatex` as well as `bibtex` run normally in git bash, so feel free to use the same git bash for both compiling and version control.

<a id="make-latex-easier-in-sublime-text"></a>
### Make LaTeX easier in Sublime Text:

- Install Package Control.
- Install LaTeXTools plugin.

https://tex.stackexchange.com/a/85487

If you have the LaTeXTools plugin, it already does that except that it is mapped on Shift+Enter instead of Enter.

<a id="shell-scripting-for-convenience"></a>
## Shell Scripting for convenience

When it comes down to it, specially when working with LaTeX or git, you find yourself making the same commands over and over again. That takes time and frustration, so I find that making scripts from time to time saves me a lot of time in the future.


<a id="basic-flag-setup-with-getopts"></a>
### Basic flag setup with getopts

Once in a while those scripts will need some input to be more useful in as many cases as possible instead of a one time thing.

Looking for how to do this I ran across [a simple StackOverflow question](https://stackoverflow.com/questions/14447406/bash-shell-script-check-for-a-flag-and-grab-its-value), which led me to the `getopts` package and its tutorial:

[Getopts manual](https://archive.ph/TRzn4)

This is a working example:

```
while getopts ":a:" opt; do
  case $opt in
    a)
      echo "-a was triggered, Parameter: $OPTARG" >&2
      ;;
    \?)
      echo "Invalid option: -$OPTARG" >&2
      exit 1
      ;;
    :)
      echo "Option -$OPTARG requires an argument." >&2
      exit 1
      ;;
  esac
done

```

<a id="argparse-bash-by-nhoffman"></a>
### Argparse-bash by nhoffman

Now sometimes you'll want to have fancy arguments with both a shortcut name (-) and a long name (--), for example `-a` and `--doall` both pointing to the same command. In that case I recommend using nhoffman's implementation of Python's `argparse` in bash:

[argparse.bash by nhoffman on GitHub](https://github.com/nhoffman/argparse-bash)

<a id="latex-helpers"></a>
### LaTeX helpers

Personally, I find it tiring to try to compile a LaTeX document, only to have to run the bibliography, and then compile the document twice again so all the references are well put where they need to be, rather tiring. Also, I find that the output files are cluttering my space and I only need to see them when I run into certain errors.

Also, for academic papers, I used `latexdiff` commands quite a lot, and while customizable, I noticed I needed a certain configuration for most journals and that was it.

So I made [LaTeX helpers](https://github.com/elisa-aleman/latex_helpers), a couple of bash scripts that make that process faster.

So instead of typing

```
pdflatex paper.tex
bibtex paper
pdflatex paper.tex
pdflatex paper.tex
open paper.tex
rm paper.log paper.out paper.aux paper.... and so on
```

Every. Single. Time. 

I just need to type:
```
./latexcompile.sh paper.tex --view --clean
```

and if I needed to make a latexdiff I just:

```
./my_latexdiff.sh paper_V1-1.tex paper.tex --newversion="2" --compile --view --clean
```

And there it is, a latexdiff PDF right on my screen.

I would also commonly have several documents of different languages, or save my latexdiff command in another script, called `cur_compile_all.sh` or `cur_latexdiff.sh` so I didn't have to remember version numbers and stuff when working across several weeks or months.

Usually with code such as:

```
cd en
./latexcompile.sh paper.tex --view --clean --xelatex
cd ../es
./latexcompile.sh paper.tex --view --clean --xelatex
cd ../jp
./latexcompile.sh paper.tex --view --clean --xelatex
```

And so on, to save time.

<a id="install-pandoc-to-convertexport-markdown-html-latex-word"></a>
## Install Pandoc to convert/export markdown, HTML, LaTeX, Word

I discovered this tool recently when I was asked to share a PDF of my private GitLab MarkDown notes. Of course I wouldn't share the whole repository so that it can be displayed in GitLab for them, so I searched for an alternative. 

It can be installed in Windows, macOS, Linux, ChromeOS, BSD, Docker, ... it's really portable

Pandoc Install:  
https://pandoc.org/installing.html


Pandoc Manual:  
https://pandoc.org/MANUAL.html


Export to PDF syntax
```
pandoc test1.md -s -o test1.pdf
```

Note that it uses LaTeX to convert to PDF, so UTF-8 languages (japanese, etc.) might return errors.

```
pandoc test1.md -s -o test1.pdf --pdf-engine=xelatex
```

But it doesn't load the Font for Japanese... Also, the default margins are way too wide.

So, in the original markdown file preamble we need to add [Variables for LaTeX](https://pandoc.org/MANUAL.html#variables-for-latex):

```
---
title: "Title"
author: "Name"
date: YYYY-MM-DD
<!-- add the following -->
geometry: margin=1.5cm
output: pdf_document
CJKmainfont: IPAMincho
---
```

And voilà, the markdown is now a PDF.

I'm still unsure if it will process the GitHub or GitLab math environments, since the syntax is different.

Upon confirmation with the [User's Guide: Math](https://pandoc.org/MANUAL.html#math) section, it uses the GitHub math syntax.

Inline: `$x=3$`  
Renders as:  
$x=3$


Block:  `$$x=3$$`  
Renders as:  
$$x=3$$


<a id="accessibility-stuff"></a>
## Accessibility Stuff

<a id="accessible-color-palettes-with-paletton"></a>
### Accessible Color Palettes with Paletton 

When designing new things it's important to keep in mind color theory, as well as accessibility for the visually impaired and color blind people, etc. But that's so much time one could spend doing so much else, so here's a tool that can help with that and also visualizing how other people with different ranges of color vision would perceive it. It's called Paletton.

https://paletton.com

<a id="reading-tools-for-neurodivergent-people"></a>
### Reading tools for Neurodivergent people

There was a new tool developed called "Bionic Reading", which bolds the beginnings of words so that our eyes glide over them more easily, basically making a tool for speed reading without having to train specifically for that. Lots of neurodivergent people such as myself (I have ADHD and am autistic), have a hard time following long texts or focusing when there is too much information at the same time (say, with very small line spacing). This new tool has been praised by the ND (neurodivergent) community, since making it available for businesses or companies to use would mean more accessibility in everyday services...  or at least it was until they decided to charge an OUTRAGEOUS amount of money to implement it, making it obviously not attractive for companies to implement and therefore ruining it for everyone.

That is why someone decided to make "Not Bionic Reading" which is, legally speaking, not the same thing as Bionic Reading and therefore can be made available for everyone as Open Source.

Here's the usable link:
https://not-br.neocities.org/

Have fun reading!

<a id="reading-white-pdfs"></a>
### Reading white PDFs

<a id="firefox"></a>
#### Firefox

https://pncnmnp.github.io/blogs/firefox-dark-mode.html

> After hunting on the web for about 30 minutes, I found this thread on Bugzilla. It turns out starting with Firefox 60, extensions are no longer allowed to interact with the native pdf viewer. Determined, I decided to locally modify the CSS rendered by Firefox's PDF viewer. The steps for the same are:
>
> - Open Firefox and press Alt to show the top menu, then click on Help → Troubleshooting Information
> - Click the Open Directory button beside the Profile Directory entry
> - Create a folder named chrome in the directory that opens
> - In the chrome folder, create a CSS file with the name userContent.css
> - Open the userContent.css file and insert -

```
#viewerContainer > #viewer > .page > .canvasWrapper > canvas {
    filter: grayscale(100%);
    filter: invert(100%);
}
```
s
> - On Firefox's URL bar, type about:config.
> - Search for toolkit.legacyUserProfileCustomizations.stylesheets and set it to true.
> - Restart Firefox and fire up a PDF file to see the change!

<a id="microsoft-edge"></a>
#### Microsoft Edge

If you ever need to read a PDF on the Microsoft Edge browser, you can create a snippet to execute on the Dev Console, as per this post.

https://www.reddit.com/r/edge/comments/nhnflv/comment/hgejdwz/?utm_source=share&utm_medium=web2x&context=3

> So, I've wanted this feature pretty badly as well and I've found a workaround which doesn't involve inverting the whole OS but still takes some extra steps:
>
> 1. Open the PDF you want to read
> 2. Right click > Inspect Element
> 3. Select Console tab
> 4. Paste the code given below
> 5. Hit enter
> 6. Profit!


```
let backgroundColor = PDFViewer.EDGE_PDFVIEWER_BACKGROUND_COLOR_LIGHT;
viewer.plugin_.setAttribute('background-color', backgroundColor);
viewer.pluginController_.postMessage({
    type: 'backgroundColorChanged',
    backgroundColor
});
document.getElementById('document-container').style.filter = 'invert()';
document.getElementById('layout-container').style.filter = 'invert()';
```

> You can utilize the snippets feature in DevTools to save the above code. To do that, do:
> 
> 1. Hit F12 or Ctrl + Shift + I to open DevTools
> 2. Once the DevTools is open, press Ctrl + Shift + P and type "new snippet" and choose the first option
> 3. Paste the above code
> 4. Right click "Script snippet #2" > Rename > "dark mode pdf"
> 5. Hit enter to rename
> 6. Close DevTools
> 
> If you did the above to save that script, the next time, you can perform the following steps to activate dark mode:
> 
> 1. Open PDF
> 2. Right click > Inspect Element
> 3. Press Ctrl + P
> 4. Type exclamation "!"
> 5. Hit enter (or select the snippet if you have multiple and press enter)

<a id="google-chrome"></a>
#### Google Chrome

I found a solution in this post:

https://superuser.com/a/1527417


> The following snippet adds a div overlay to any browser tab currently displaying a PDF document.
> 1. Open up your browser's Dev tools then browser console.
> 2. Paste this JavaScript code in your browser console:

```
const overlay = document.createElement("div");

const css = `
    position: fixed;
    pointer-events: none;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    background-color: white;
    mix-blend-mode: difference;
    z-index: 1;
`
overlay.setAttribute("style", css);

document.body.appendChild(overlay);
```

> 3. Hit Enter
>
> Special thanks: https://www.reddit.com/r/chrome/comments/e3txhi/comment/fem1cto


---

That is all for now. This is my initial setup for the development environment. If I have any projects that need further tinkering, that goes on another repository / tutorial.

