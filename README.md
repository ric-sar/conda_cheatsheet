![conda_logo](https://github.com/ric-sar/conda_cheatsheet/assets/82369153/632272e9-b7a3-4b70-bff0-604977b686d8)

<div align="center">This repo is meant to be a useful non-comprehensive Conda Cheat Sheet.<br>
For starters, I recommend to read first <a href="https://conda.io/projects/conda/en/latest/user-guide/getting-started.html">Getting started with conda</a>
</div>

---

**Table of contents**
- [Create new environment](#create-new-environment)
  * [List environments](#list-environments)
  * [Clone from other environment](#clone-from-other-environment)
  * [Import from yaml file](#import-from-yaml-file)
- [Export environment](#export-environment)
- [Activate or deactivate environment](#activate-or-deactivate-environment)
- [Update environment](#update-environment)
- [Install and unistall package](#install-and-unistall-package)
  * [Using pip](#using-pip)
  * [Using conda](#using-conda)
  * [List all packages in the environment](#list-all-packages-in-the-environment)
  * [Search package](#search-package)
- [Remove environment](#remove-environment)
- [Rename environment](#rename-environment)
- [Uninstalling Anaconda distribution](#uninstalling-anaconda-distribution)

# Create new environment
```
conda create --name ENVNAME
```
## List environments
```
conda env list
```

## Clone from other environment
```
conda create --name ENVNAME --clone base
```
## Import from yaml file
```
conda env create -n ENVNAME --file ENV.yml
```
or if the ENVNAME is already in the yml file:
```
conda env create -f environment.yml
```

# Export environment
```
conda env export > environment.yml
```

# Activate or deactivate environment
To activate an environment:
```
conda activate ENVNAME
```

To deactivate an environment:
```
conda deactivate ENVNAME
```

# Update environment
```
conda update --all
```

# Install and unistall package
## Using pip
```
pip install PACKAGENAME
```

```
pip uninstall PACKAGENAME
```

## Using conda
```
conda install PACKAGENAME
```

```
conda remove PACKAGENAME
```
## List all packages in the environment
```
pip list
```

```
conda list
```

## Search package
```
pip search PACKAGENAME
```
But sometimes you partially remember the package-name and you can use regex:
```
pip search PACKAGENAME
```
*** Da verificare i due comandi sopra ***

In conda you don't need to specify the package name, it will use automatically regex:
```
conda list PACKAGENAME
```

# Remove environment
```
conda remove -n ENVNAME --all
```

# Rename environment
```
conda rename -n ENVNAME NEWENVNAME
```


 
# Uninstalling Anaconda distribution
https://docs.anaconda.com/free/anaconda/install/uninstall/
