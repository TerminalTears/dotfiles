# dotfiles

If it's your first time using Github on the terminal, you need to first open a terminal
run the following commands:

Example:
$ git config --global user.name "Your name here"
$ git config --global user.email "your_email@example.com"


Create a directory somewhere called 'dotfiles'.
Copy your original dotfiles to this directory.
Replace the original dotfiles with symlinks. Ensure to use absolute paths in the ln command.
-s creates a symbolic link -f forces forces the removal of existing destination files.
If you have a lot of dotfiles, consider creating a script to create the symbolic links.

Example:
$ ln -sf ~/dotfiles/.bashrc ~/.bashrc

Push the files to your repository.
$ git init
$ git add .
$ git commit -m ‘first commit’
$ git remote add origin https://github.com/yourname/dotfiles
$ git push origin master

You may get an error about unrelated histories when running 'git push origin master' for the 
first time. In order to get around this, you first have to run the following command.
$ git pull origin master --allow-unrelated-histories

Now you can run the push command again.
$ git push origin master

Referece:
https://github.community/t/how-to-deal-with-refusing-to-merge-unrelated-histories-error/1372
