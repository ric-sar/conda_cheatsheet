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
- [Install and uninstall package](#install-and-uninstall-package)
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
or if the ```ENVNAME``` is already in the yml file:
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

# Install and uninstall package
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
Sometimes you need to look for an installed package inside a specified environment. This can be achieved by using the command ```list``` followed by the ```PACKAGENAME```: 
```
conda list PACKAGENAME
```
If you don't remember the ```PACKAGENAME``` conda introduce some regex-like search. For example if you remember only the first letters of ```PACKAGENAME``` you can use ```list``` command followed by hyphen and the first letters. For example you look for ```sci``` packages:
```
conda list ^sci
```

```
# Name                    Version                   Build    Channel
scikit-image              0.19.3           py39hd77b12b_1
scikit-learn              1.2.1            py39hd77b12b_0
scikit-learn-intelex      2023.0.2         py39haa95532_0
scipy                     1.10.0           py39h321e85e_1
```

Alternatively, if you 'by specifing only typing part of ```PACKAGENAME```. The following command will show all the packages with name ```torch``` inside:
```
# Name                    Version                  Build     Channel
pytorch                   1.13.1             py3.9_cpu_0     pytorch
pytorch-mutex             1.0                        cpu     pytorch
torchaudio                0.13.1                py39_cpu     pytorch
torchvision               0.14.1                py39_cpu     pytorch
```
As you can see, conda lists the name, version, build and channel (where the repository come from).

# Remove environment
```
conda remove -n ENVNAME --all
```

# Rename environment
```
conda rename -n ENVNAME NEWENVNAME
```

# Uninstalling Anaconda distribution
To make a clean uninstallation of the Anaconda distribution you must have installed the ```anaconda-clean``` package inside the base environment:
```
conda install anaconda-clean
```
Then, run the command:
```
anaconda-clean --yes
```
This command will create a backup of all files and directories that might be removed in a folder named ```.anaconda_backup```
At the end of the process you can delete all the Anaconda-related folders, for envs(```anaconda3\envs```) and packages(```anaconda3\pkgs```).

[Check the documentation for more details](https://docs.anaconda.com/free/anaconda/install/uninstall/)
