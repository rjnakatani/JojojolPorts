# JojojolPorts
Local Portfile Repository for Jojojol based on [Funalab Ports](https://github.com/funasoul/FunalabPorts/).

## What is here
* python/py-optuna  ... Portfile for [optuna](https://pypi.org/project/optuna/) v2.10.0
* python/py-cmaes  ... Portfile for [cmaes](https://pypi.org/project/cmaes/) v0.8.2

## How to use
### Use this project as your Local Portfile Repository
At first, clone this project.
```sh
% mkdir -p ~/git
% cd ~/git
% git clone https://github.com/rjnakatani/JojojolPorts
% cd JojojolPorts
% portindex
```
Then, add this local repo. to your MacPorts.
```sh
% sudo chmod 644 /opt/local/etc/macports/sources.conf
% sudo vim /opt/local/etc/macports/sources.conf
# Add this following line (please change "yourname" as your username)
file:///Users/yourname/git/JojojolPorts
% sudo chmod a-w /opt/local/etc/macports/sources.conf
```

### Test whether your Macports can find your local repo.
```sh
% port search optuna
```

### Install py-optuna (2.10.0) by MacPorts
```sh
% sudo port install py38-optuna
```
or
```sh
% sudo port upgrade py38-optuna
```
