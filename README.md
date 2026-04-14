# Conda-environment-setup-for-beginners-from-USC
Hi everyone, welcome to this post! This tutorial is situable for beginners who are from University of Southern California, curious of how Bioinformatics/Cheminformatics tools are loaded on the USC CARC (more specifically, discovery cluster).

## Introduction to Vim and `.bashrc` File 
**The goal of introducing Vim is that we are able to modify our ".bashrc" file for envrionment setup**
### What is Vim and how to use Vim
For very beginners, it might disturbs you for creating/modifying a file on the USC Discovery cluster. Although there is a way of transferring files from your local machine to Discovery (https://www.carc.usc.edu/user-guides/hpc-systems/discovery/getting-started-discovery), yet it is really inconvenient and isn't situable for every situation. To creating/modifying a file, there are text editors avaliable. They serve as a txt file editor in the Linux operating system: 

Micro: https://micro-editor.github.io/

Nano: https://www.nano-editor.org/

Vim: https://www.vim.org/

Emacs: https://www.gnu.org/software/emacs/

We will quickly go through the basic usage of Vim. To open a file, type `vim <your_filename>`; to change the position of the cursor, use arrow keys on your keyboard (←, →) to shift left or right, while arrow keys (↑, ↓) are for moving up a line or moving down a line; enter the edit mode and start inserting text before the current cursor position, type `i`; to quit the edit mode, press your "esc" key; to save your changes, type `:q`.

### What is `.bashrc` file
The .bashrc file is a user-specific configuration script that runs every time you open a new interactive terminal (That is to say, the .bashrc file runs everytime when we log into Discovery). It’s used to set up a personalized environment by defining:

Environment variables: set paths and configurations (e.g., relied libraries) for other programs

Command aliases: shortcuts for your most-used commands

Shell functions: more complex, custom commands that can accept arguments

### Where to find `.bashrc` file
The Linux .bashrc file is mostly located in your user’s home directory(`/home1/your_USCusername`). You can find and open it from the command line.

To view the file, use `ls -a` in your home directory to see all the hidden files.

### Editing `.bashrc` file
To edit, type `vim ~/.bashrc` (Notification: ~ represents for your home directory)

To make what you have edited work, type `source ~/.bashrc` so that it will immediately work in your current login shell. If you close the current shell(terminal), and open a new one, it will automatically load the modified one.

## Use `module load conda` to download conda
### Why do we need conda to download softwares? Can't we just directly download softwares using `wget`? 

The advantage of using conda is illustrated in:
https://hpcc.umd.edu/software/conda/

Before starts, make sure there is no already existed conda environment in your `.bashrc` file. You shouldn't seen there is a section called `# >>> conda initialize >>>`, this should not exit at all:

<img width="2098" height="1576" alt="image" src="https://github.com/user-attachments/assets/fd07d9f1-32e4-4768-a9f5-fc3b670f7d23" />

### `module load` command 
`module load` which allows you load all ready setup softwares, which are deliberately packaged and compiled to be aligned with the current linux core(GNC version). We will stick with the conda version that USC Cluser provided.

To use Conda, first load the corresponding module:
`module load conda`

However, merely by loading conda means that you have to do this everytime when you login to Discovery. We can add this command into `.bashrc` file to load the conda permanently. 


## Conda Initial Setup
## Example of Downloading AutodockTools and AutoGrid through conda


