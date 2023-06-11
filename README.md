![conda_logo](https://github.com/ric-sar/conda_cheatsheet/assets/82369153/27cac864-5035-461b-afb1-31d1f6347459)

<div align="center">This repo is meant to be a useful non-comprehensive Conda Cheat Sheet.<br>
For starters, I recommend to read first <a href="https://conda.io/projects/conda/en/latest/user-guide/getting-started.html">Getting started with conda</a>
</div>

---

**Table of contents**
- [What is conda](#what-is-conda)
- [Create new environment](#create-new-environment)
  * [List environments](#list-environments)
  * [Clone from other environment](#clone-from-other-environment)
  * [Import from YAML file](#import-from-yaml-file)
- [Export environment](#export-environment)
- [Activate or deactivate environment](#activate-or-deactivate-environment)
- [Update environment](#update-environment)
- [Install and uninstall package](#install-and-uninstall-package)
  * [Using pip](#using-pip)
  * [Using conda](#using-conda)
  * [List all packages in the environment](#list-all-packages-in-the-environment)
  * [Search package](#search-package)
  * [List outdated packages](#list-outdated-packages)
- [Remove environment](#remove-environment)
- [Rename environment](#rename-environment)
- [Uninstalling Anaconda distribution](#uninstalling-anaconda-distribution)

# What is conda
Conda is a cross-platform environment and package management system. It allows you to create, delete, update, clone, import, export environments and install, uninstall, search, update packages while solving [dependency hell](https://en.wikipedia.org/wiki/Dependency_hell).
This repo is based on [Anaconda Distribution](https://www.anaconda.com/), a popular conda distribution that contains 1,500 scientific packages, pip, Python and of course conda. You can apply the cheat sheet also on miniconda, a "smaller" version of Anaconda that contains a smaller amount of packages, pip, Python and conda.

[Have a look at this comparison between Anaconda and miniconda](https://docs.conda.io/projects/conda/en/stable/user-guide/install/download.html#anaconda-or-miniconda)

# Create new environment
If you want to create an empty environment you can use the ```create``` command followed by the ```$ENVNAME``` and specifying that you don't want any package installed:
```
conda create --name $ENVNAME --no-default-packages
```
Of course you can create a new environment with a specified Python version or packages to install:
```
conda create --name $ENVNAME python=3.8
```

## List environments
If you want to list all the available environments install, use the command ```env list```:
```
conda env list
```
This command will put all the environments and location:
```
# conda environments:
base         *           C:\Users\Riccardo\anaconda3
env_1                    C:\Users\Riccardo\anaconda3\envs\env_1
env_2                    C:\Users\Riccardo\anaconda3\envs\env_2
env_3                    C:\Users\Riccardo\anaconda3\envs\env_3
```
As you can see there is a ```*``` near the ```base environment```, this will help you to understand the environment in use in that moment.

## Clone from other environment
Sometimes you have already setup an environment used as baseline and want to add new packages, this procedure can be done by cloning a specified environment. You have to use the same ```create``` command followed by the environemtn to clone with ```--clone``` command:
```
conda create --name $ENVNAME --clone base
```

## Import from YAML file
YAML is a human-readable data-serialization language mainly used as configuration file. In our case, ```.yml``` file contains all the required packages to create and reproduce an environment.
With standard command create by imposing the ```.yml``` file path we can create a new environment as described internally in the `.yml` configuration:
```
conda env create -n $ENVNAME --file $ENV.yml
```
If the ```$ENVNAME``` has been already specified inside the ```.yml``` file, we can just remove the ```-n $ENVNAME``` part:
```
conda env create -f environment.yml
```

# Export environment
Sometimes you need to export your environment with all the required packages, this is extremely useful we want to setup the same environment on another pc/server/whatever.
In this case just use the ```export``` command followed by destination path of the ```.yml``` configuration file:
```
conda env export > environment.yml
```

# Activate or deactivate environment
After setup many environments maybe you need a command to activate or deactivate a particular one. The commands are pretty straight forward, use ```activate``` command followed by the ```$ENVNAME``` to activate an environment:
```
conda activate $ENVNAME
```
Instead, if you want to deactivate the environment just type ```deactivate``` command followed by the ```ENVNAME```:
```
conda deactivate $ENVNAME
```

If you want to deactivate and environment and activate another one you don't really need to deactivate the environment first but you can actually activate the environment by just using the ```activate``` command, the previous environment will be deactivated. 

# Update environment
Conda as package manager can update all the depencies easily with the ```update``` command:
```
conda update --all
```
Please note that conda will only update packages installed by conda and not the one installed by ```pip```. To upgrade a package in pip please use the following command:
```
pip install --upgrade $PACKAGENAME
```
It is possible to update all the pip packages but it is not recommended due to the complexity to handle environment checks in pip.

# Install and uninstall package
Conda as package manager can be useful to install or uninstall packages. Inside a conda environment you can install packages with the standard package manager for Python (```pip```).
Let's have a look at pip and then conda:

## Using conda
Use the command ```install``` followed by the ```$PACKAGENAME``` to install it:
```
conda install $PACKAGENAME
```
Use the command ```remove``` followed by the ```$PACKAGENAME``` to uninstall it:
```
conda remove $PACKAGENAME
```

## Using pip
The same che be applied to pip package manager. Please use the ```install``` command to install a package:
```
pip install $PACKAGENAME
```
Use the ```uninstall``` command followed by the ```$PACKAGENAME``` to uninstall it:
```
pip uninstall $PACKAGENAME
```

## List all packages in the environment
To list all the packages installed in the environment just simply use:
```
conda list
```
The output will be a list of packages with: name, version, build and channel (where the repository come from):
```
Name                      Version                     Build    Channel
pytorch                   2.0.0    py3.10_cuda11.7_cudnn8_0    pytorch
pytorch-cuda              11.7                   h16d0643_3    pytorch
...
tensorboard               2.12.2               pyhd8ed1ab_0    conda-forge
...
torchaudio                2.0.0                      pypi_0    pypi
torchvision               0.15.0                     pypi_0    pypi
```

## Search package
Sometimes you need to look for an installed package inside a specified environment. This can be achieved by using the command ```list``` followed by the ```$PACKAGENAME```: 
```
conda list $PACKAGENAME
```
If you don't remember the ```$PACKAGENAME``` conda introduces some regex-like search. For example if you remember only the first letters of ```$PACKAGENAME``` you can use ```list``` command followed by hyphen and the first letters. For example you look for ```sci``` packages:
```
conda list ^sci
```
The output will be a list of packages with: name, version, build and channel (where the repository come from).
```
Name                      Version                   Build    Channel
scikit-image              0.19.3           py39hd77b12b_1
scikit-learn              1.2.1            py39hd77b12b_0
scikit-learn-intelex      2023.0.2         py39haa95532_0
scipy                     1.10.0           py39h321e85e_1
```
If you remember only part of packagename, does not matter if the beginning, the middle or the end of ```$PACKAGENAME```, just type what you remember after ```list``` command.
The following command will show all the packages with name ```torch``` inside:
```
Name                      Version                  Build     Channel
pytorch                   1.13.1             py3.9_cpu_0     pytorch
pytorch-mutex             1.0                        cpu     pytorch
torchaudio                0.13.1                py39_cpu     pytorch
torchvision               0.14.1                py39_cpu     pytorch
```
Also, multiple ```$PACKAGENAME``` search can be applied by concatenating names or part of the name with a pipe |. The following command will show all packages that contains ```sci``` and ```torch```:

```
conda list "(sci|num)"
```
The output will be a combination of the two search:
```
Name                      Version                  Build     Channel
pytorch                   1.13.1             py3.9_cpu_0     pytorch
pytorch-mutex             1.0                        cpu     pytorch
scikit-image              0.19.3          py39hd77b12b_1
scikit-learn              1.2.1           py39hd77b12b_0
scikit-learn-intelex      2023.0.2        py39haa95532_0
scipy                     1.10.0          py39h321e85e_1
torchaudio                0.13.1                py39_cpu     pytorch
torchvision               0.14.1                py39_cpu     pytorch
```

## List outdated packages
### Using conda
To list all packages to update inside an environment please use the ```search``` command:
```
conda search --outdated
```

### Using pip
The same apples to search for all ```pip``` installed packages:
```
pip list --outdated
```

# Remove environment
If you want to delete an environment you can use the ```remove``` command as the following:
```
conda remove -n $ENVNAME --all
```
By applying ```--all``` you will remove all the packages related to the environment.

# Rename environment
To rename an environment just use the command ```rename``` followed by the environment you want to rename (```$ENVNAME```) and the name (```$NEW_ENVNAME```) to apply to it:
```
conda rename -n $ENVNAME $NEW_ENVNAME
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
