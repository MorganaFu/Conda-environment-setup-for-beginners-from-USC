# Conda-environment-setup-for-beginners-from-USC

Hi everyone, welcome to this tutorial! This guide is suitable for beginners from the University of Southern California who are curious about how Bioinformatics/Cheminformatics tools are set up on the USC CARC Discovery cluster.

## Introduction to Vim and `.bashrc` File 
**The goal of this section is to learn how to modify our `.bashrc` file for environment setup using Vim.**

### What is Vim and how to use Vim
For complete beginners, creating or modifying a file directly on the USC Discovery cluster can feel unfamiliar. Although there is a way to transfer files from your local machine to Discovery (https://www.carc.usc.edu/user-guides/hpc-systems/discovery/getting-started-discovery), it is inconvenient and not suitable for every situation. Instead, you can use a terminal-based text editor. Several options are available for Linux:

Micro: https://micro-editor.github.io/

Nano: https://www.nano-editor.org/

Vim: https://www.vim.org/

Emacs: https://www.gnu.org/software/emacs/

We will quickly go through the basic usage of Vim. To open a file, type `vim <your_filename>`; to change the position of the cursor, use arrow keys on your keyboard (←, →) to shift left or right, while arrow keys (↑, ↓) are for moving up a line or moving down a line; to enter edit (insert) mode and start typing, press `i`. To exit edit mode, press Esc. To save your changes, type `:w`. To save and quit, type `:wq`. To quit without saving, type `:q!`.

⚠️ Note: `:q` alone will only quit if no unsaved changes exist. Use `:wq` to save and quit.

### What is `.bashrc` file
The .bashrc file is a user-specific configuration script that runs every time you open a new interactive terminal (That is to say, the .bashrc file runs everytime when we log into Discovery). It’s used to set up a personalized environment by defining:

Environment variables: set paths and configurations (e.g., required libraries) for other programs

Command aliases: shortcuts for your most-used commands

Shell functions: more complex, custom commands that can accept arguments

### Where to find `.bashrc` file
The .bashrc file is located in your home directory (/home1/your_USCusername). To confirm it exists, run `ls -a` in your home directory to list all files, including hidden ones (files starting with .).

### Editing `.bashrc` file
To open and edit it, type: 

`vim ~/.bashrc` 

(Notification: `~` is shorthand for your home directory.)

After making changes, run:

`source ~/.bashrc`

This applies your changes immediately in the current session. Any new terminal session you open afterward will also load the updated .bashrc automatically.

## Using `module load conda` to set up Conda
### Why do we need conda to download softwares? Can't we just directly download softwares using `wget`? 

The advantage of using conda is illustrated in:
https://hpcc.umd.edu/software/conda/

Before starts, make sure there is no already existed conda environment in your `.bashrc` file. You shouldn't seen there is a section called `# >>> conda initialize >>>`— if it is already there, Conda may have been previously initialized and this setup may conflict:

<img width="2098" height="1576" alt="image" src="https://github.com/user-attachments/assets/fd07d9f1-32e4-4768-a9f5-fc3b670f7d23" />

### `module load` command 
`module load` allows you to load pre-installed software that has been deliberately packaged and compiled to be compatible with the current Linux system libraries and GNU compiler version. We will use the Conda version provided by the USC cluster.

To use Conda, first load the corresponding module:
`module load conda`

However, this command only applies to your current session — you would need to re-run it every time you log into Discovery. To avoid this, add the command to your .bashrc file so that Conda is loaded automatically at the start of every login session. 

Run the following command to write a **new** `conda initialize` block into your .bashrc that is correctly linked to the school's high-performance module conda

`conda init bash`

`source ~/.bashrc`

 Here’s how to **prove which underlying `conda` executable** the function is dispatching to:
 `type -a conda`

 You should've see:
 `conda is /apps/conda/miniforge3/25.11.0-1/bin/conda`

 Since the conda is in `/apps/`, representing for it is maintained by the USC CARC admins. 

## Installing Conda environments

You can create Conda environments within any of your accessible directories, such as your home (/home1) or project (/project) directories. These environments are isolated workspaces designed to manage specific package versions and dependencies independently for different projects.

This isolation allows you to run multiple programs with conflicting requirements on the same system. For example, if one workflow requires Python 2.7 (like AutoDock Tools) while another requires Python 3.12, you can maintain two separate environments. Switching between them ensures that the libraries for one project never interfere with or break the other.

The process for creating and using environments has a few basic steps:

Create an environment with `conda create`
Activate the environment with `conda activate`
Install packages(programs) into the environment with `conda install`

To create a new Conda environment in **your home directory**, enter:

`conda create --name <env_name>`

where <env_name> is the name your want for your environment. Then activate the environment:

`conda activate <env_name>`

To deactivate an environment, enter:

`conda deactivate`

You can also create a new environment in **your project directory** using the --prefix option. For example:

`conda create --prefix /project2/ttrojan_123/<env_name>`

Then activate the environment:

`conda activate /project2/ttrojan_123/<env_name>`

## Example of installing Autodock4/Vina, AutoGrid and AutoDockTools(GUI for Autodock4/Vina) through conda


