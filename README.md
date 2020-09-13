
## dotfiles

I decided to keep a repository of my dotfiles to preserve my favorite settings for bash, tmux, vim, etc. This README will walk you through the steps on how to do that from scratch.

---
If it's your first time using git on the terminal, you need to first make sure you have registered an account
on Github and created a repository for your docfiles open a terminal run the following commands:

***Example***:

    $ git config --global user.name "Your name here"
    $ git config --global user.email "your_email@example.com"

---

**Step 1.)** Create a directory on your machine to store your docfiles. I chose a directory named 'dotfiles'.

    $ mkdir ~/.dotfiles

**Step 2.)** Copy your original dotfiles to the newly created directory.

    $ cp ~/.bashrc ~/.dotfiles

**Step 3.)** Replace the original dotfiles with symlinks. Ensure to use absolute paths in the command.
The -s and -f options creates a symlink and forces the removal of existing destination files, respectively.
If you have a lot of dotfiles, consider creating a script to create the symbolic links for you so you can just
run the script on a freshly installed system.

    $ ln -sf ~/dotfiles/.bashrc ~/.bashrc

**Step 4.)** From the dotfiles directory, push the files to your repository.

    $ git init
    $ git add .
    $ git commit -m ‘first commit’
    $ git remote add origin https://github.com/yourname/dotfiles
    $ git push origin master

**Circumventing "Fatal: refusing to merge unrelated histories" error**
You may get an error about unrelated histories when running the 'git push origin master' command for the 
first time. In order to get around this, use the following commands.

    $ git pull origin master --allow-unrelated-histories
    $ git push origin master

**Additional Notes**
If you want to clone this entire repository, do it in the **~** directory. The files in directories should be symbolically linked to their respective files on the target system. For example, the file (in this repository) **/etc/vim/vimrc.local** would link to **/etc/vim/vimrc.local** on the target machine. This was done as a way to remember where each symlink needs to be created. Files in the root directory of this repository should be linked to the **~** with their respective filenames.
