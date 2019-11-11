## General tips, tricks and shortcuts ##

# Change bash command prompt to show current working directory
```
# Add to .bashrc

PS1="\[\`if [[ \$? = "0" ]]; then echo '\e[32m\h\e[0m'; else echo '\e[31m\h\e[0m' ; fi\`:\$PWD\n\$ "
```

# Create a symbolic link between bash script in another folder and bin
Make sure the script is executable in the original folder. By creating a soft link (-s flag) any changes made to the original script will be reflected when running script via bin.

```
ln -s /path/to/original/script.sh ~/bin
```
# Add tab-bar when working within `screen`

When you have multiple `screen` sessions running it's easy to lose track of where you are. This .screenrc profile from https://github.com/UofABioinformaticsHub/nathan_sysadmin_scripts/blob/master/phoenix/rc/.screenrc adds a tab-bar at the bottom.  

```
# Add or create ~/.screenrc with the below

startup_message off
caption string "%?%F%{= Bk}%? %C%A %D %d-%m-%Y %{= kB} %t%= %?%F%{= Bk}%:%{= wk}%? %n "
hardstatus alwayslastline
hardstatus string '%{= kG}[ %{G}%H %{g}][%= %{= kw}%?%-Lw%?%{r}(%{W}%n*%f%t%?(%u)%?%{r})%{w}%?%+Lw%?%?%= %{g}][%{R} %d/%m %{W}%c %{g}]'
altscreen on
# Let screen spawn its shell as the user's login shell. This will then also parse /etc/profile /etc/profile.d and ~/.profile
shell -$SHELL

# When starting a screen session:

screen -t mysessionname -S mysessionname

# that means the title (-t) with be added to the tab-bar and using -S means when you run `screen -ls` you can easily identify your session name
```

# Create a git repo of .bashrc and .bash_profile

If you create a repo of all your configuration files, when you need to set up a new computer you can easily create the same system setup. 

However, git doesn't track hidden (.) files as standard, so you need to create a new folder i.e. `dotfiles` and create a symbolic link with the original config files. Push the `dotfiles` folder to git and it should contain the original config files. 

# Create aliases

To speed thing up shorten long commands into aliases saved in the .bashrc file. For example:

```
alias push="git push origin master"
alias pull="git pull origin master"
```

# Copy and paste via ubuntu without mouse

Check out this article: https://www.ostechnix.com/how-to-use-pbcopy-and-pbpaste-commands-on-linux/

You can copy file from shell onto the clipboard by piping to pbcopy:

```
cat test_texfile.txt | pbcopy

# to paste the text

pbpaste
```

# Automatically ls contents of directory when cd

Create a new function that when entered into the terminal will both `cd` then `ls` of current dir.

Add following to .bashrc

```
cdls() { cd "$@" && ls; }
```
New function is called `cdls`. `&&` means if the first command is true then `ls` is performed.

# How to find a file within a directory

If you need to find a file but can't remember exactly which subfolder it's saved in:

```
find <filepath> -name "filename"

# eg to find all snakemake files in my bin folder

find ~/bin -name *.smk

# search for specific file in entire home directory

find ~/ -name "ITS-pulse-survey-single-snakemake.smk"

# will print the full filepath to terminal
```

You can also use the -delete flag at the end to remove the found file.

# Search contents of file in the terminal
 
`less` is simialr to `cat` in that in prints the file contents to terminal but it also lets you scroll through the file using `j` key to move down and `k` to move up. You can search for a specific word e.g. reverse by typing `/reverse` all instances of reverse will be highlighted. The quit type `q`.

`bat` downloaded from github (https://github.com/sharkdp/bat) is a pimped up version of `less` with syntax highlighting, line numbers and works with git to show file changes.

# Search file for specific pattern

Syntax of grep:

```
grep <expression> <path>
```

For example if you want to check all the conda environment rule statements within a snakemake file:

```
# To search one specific file
grep conda: /home/DAVIEL20/SAGIT_survey_2019/Snakemake/ITS-pulse-survey-single-snakemake.smk

# Search for a pattern within every subfolder and file in the home directory and show line number
grep -r conda: ~/
```
The `-n` flag adds line number.

Unlike `less` you're not working within the file itself, it's an easy way to see how many times you've stated a function before you change it. 

Pimped up version (looks much nicer) available at https://github.com/BurntSushi/ripgrep


# Move between directories on the CL

Download `z` from https://github.com/rupa/z. Enables you to move directly to your directory of interest on the CL without entering the entire filepath name i.e:

```
cd /home/DAVIEL20/Data/FungiSeq/snakemake-test-run/

# instead enter

z snakemake-test-run
```

# Listing processes and killing them

Copied from Launch School Tech Talks: Command Line Tips & Tricks (https://launchschool.com/gists/b05ad752)

![](2019-11-11-12-27-58.png)

