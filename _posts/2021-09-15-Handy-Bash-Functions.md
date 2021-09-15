---
title: "Handy Bash Functions for ML & Data Science"
description: Once I figure out a complicated command, I make a bash function for it
layout: post
toc: false
comments: true
image: images/bash_functions_thumb.png
date: 2021-09015 10:46:18
hide: false
search_exclude: false
typora-root-url: /Users/shawley
---

Once I figure out a complicated command, I make a `bash` function or alias for it.
Here are some that I find useful.
(Note that `"$1"` just refers to the first argument of the command.)

```bash

# set up python environment. usage: $ makeenv <env_name>
makeenv() { python3 -m venv ~/envs/"$1"; source ~/envs/"$1"/bin/activate; python3 -m pip install pip -Uqq; }

# loadsenv usage: $ loadenv <env_name>
loadenv() { source ~/envs/"$1"/bin/activate; }
#same thing different name
gimme() { source ~/envs/"$1"/bin/activate; }

# downloads colab notebook.  usage: $ grabcolab <sharing_URL>    [Writes to colab.ipynb]
grabcolab() { fileid=$( echo "$1" | sed -E 's/.*drive\/(.*)\?.*/\1/' ); wget -O colab.ipynb 'https://docs.google.com/uc?export=download&id='$fileid; }

# runs a notebook on command line.  usage: $ nbrun colab.ipynb.  Note for student nbs, run this from an access-reduced account!
nbrun() { pip install -Uqq jupytext; jupytext --to py "$1";  mv  "${1%.*}".py run_this.ipy; ipython run_this.ipy;}

# creates .tgz file from directory, runs in parallel; usage: $ partar <dir_name>  [no / on end]  
# requires pigz: $ sudo apt install pigz
partar() { tar -I pigz -cf "$1.tgz" "$1";  }

# uncompresses .tgz file into directory, runs in parallel. usage $ paruntar <.tgz file>
paruntar() { tar -I pigz -xf "$1";  }  

# which alias is this?  includes functions too.  usage: $ wa partar
wa() { type "$1";}
```
