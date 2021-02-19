
## Using Github for Storing Dotfiles

Dotfiles are the configuration files for your Linux system. I decided to keep a repository of my dotfiles to preserve my favorite settings for bash, tmux, vim, etc so that the same settings could easily be applied to new installations. This README will walk you through the steps on how to do that from scratch.

---
If it's your first time using git on the terminal, you need to first make sure you have registered an account
on Github and created a repository for your dotfiles. Then open a terminal run the following commands:

    $ git config --global user.name "Your name here"
    $ git config --global user.email "your_email@example.com"

---

**Step 1.)** Create a directory on your machine to store your dotfiles. I chose a directory named 'dotfiles'.

    $ mkdir ~/.dotfiles

**Step 2.)** Copy your original dotfiles to the newly created directory.

    $ cp ~/.bashrc ~/.dotfiles

**Step 3.)** Replace the original dotfiles with symlinks. Ensure to use absolute paths in the command.
The -s and -f options creates a symlink and forces the removal of existing destination files, respectively.
If you have a lot of dotfiles, consider creating a script to create the symbolic links for you so you can just
run the script on a freshly installed system.

    $ ln -sf ~/dotfiles/.bashrc ~/.bashrc
    $ ln -sf ~/dotfiles/.bash_profile ~/.bash_profile
    

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
    
**Git push origin master not pushing changes to dotfiles**
Sometimes the `git push origin master` command doesn't update the files that have been modified. First, run:
    $ git commit -m 'message'

A prompt will show up telling you which files have been modified, but are not staged for the commit. It will then list the files it is referring to. Then, run:
    $ git add <file>

Lastly, make the push
    $ git push origin master


**Additional Notes**
If you want to clone this entire repository, do it in the **~** directory. The files in directories should be symbolically linked to their respective files on the target system. For example, the file (in this repository) **/etc/vim/vimrc.local** would link to **/etc/vim/vimrc.local** on the target machine. This was done as a way to remember where each symlink needs to be created. Files in the root directory of this repository should be linked to the **~** with their respective filenames.

You might be wondering why I have created a symlink for .bash_profile despite having already linked .bashrc file. The reason for this is because when tmux starts, it sources the terminal configuration from .bash_profile. This results in a colorless terminal. The two workarounds for this- The first workaround is to add the contents of .bashrc to .bash_profile, or add a line in the .bash_profile which sources from the .bashrc file.

    $ source ~/.bashrc

---
### Removing a folder from git
If you need to remove git from a folder for any reason, use the following command in the directory that you don't need to run git. For example, if you change the repository name and you want that name change reflected in a new directory on your system.

		rm -rf .git

### Committing changes
If you modify a file you must you first commit the change before pushing it.
		
		git commit -a -m "Write a message"
