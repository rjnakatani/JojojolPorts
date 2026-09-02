# JojojolPorts
Local Portfile Repository for Jojojol based on [Funalab Ports](https://github.com/funasoul/FunalabPorts/).

## What is here
* python/py-optuna  ... Portfile for [optuna](https://pypi.org/project/optuna/) v2.10.1
* python/py-cmaes  ... Portfile for [cmaes](https://pypi.org/project/cmaes/) v0.8.2
* python/py-cliff_dev ... Portfile from [py-cliff](https://github.com/macports/macports-ports/blob/master/python/py-cliff/Portfile) with added py39 variant
* python/py-kivy_dev ... Portfile for [kivy](https://github.com/kivy/kivy/) 1.10.1
* python/py-fake-useragent ... Portfile for [py-fake-user-agent](https://github.com/fake-useragent/fake-useragent) v0.1.11
* python/py-pynverse ... Portfile for [pynverse](https://github.com/alvarosg/pynverse) v0.1.1.4
* editors/neuron-mode.el ... Portfile for [neuron-emacs](https://github.com/davidcsterratt/neuron-emacs)
* science/omega_h ... Portfile for [omega\_h](https://github.com/sandialabs/omega_h) v9.34.13
* science/steps ... Portfile for [STEPS](https://steps.sourceforge.net/STEPS/default.php) 5.0.2
* science/libsbml_dev ... Portfile for development branch [libsbml](https://github.com/sbmlteam/libsbml) v5.20.4
* devel/cmake-bootstrap-nocurses ... Fork of [cmake-bootstrap](https://github.com/macports/macports-ports/blob/master/devel/cmake-bootstrap/Portfile) with the ccmake curses GUI disabled unconditionally on Darwin, to work around a linker failure against Apple's SDK curses shim on modern macOS

## overrides/
A separate, self-contained Portfile tree kept apart from the ports above. Everything here
intentionally reuses the **same name** as an official port, so that it wins name resolution
over the official ports tree (both for `port install <name>` and for any other port's
`depends_*:port:<name>`) once its own source entry is given priority - see setup below. It is
kept in its own root (with its own `PortIndex`) rather than mixed into the main tree so that
giving it priority doesn't also activate the unrelated `_dev`-style forks above.

* overrides/devel/cmake-bootstrap ... Override of the official `cmake-bootstrap` port with the
  same ccmake curses GUI fix as devel/cmake-bootstrap-nocurses. Needed because MacPorts has no
  dependency-substitution mechanism: ports that declare `depends_*:port:cmake-bootstrap`
  (e.g. `clang-11-bootstrap`, pulled in transitively when building things like neovim/tmux's
  toolchain) can only be satisfied by a port literally named `cmake-bootstrap`.




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

### Use the overrides/ tree
`overrides/` reuses official port names on purpose, so it must be listed **above** the official
tarball source (and above the plain `JojojolPorts` line) in `sources.conf` - MacPorts uses the
first matching source it finds, so this is what makes the override actually take effect instead
of silently falling back to the official port.
```sh
% sudo chmod 644 /opt/local/etc/macports/sources.conf
% sudo vim /opt/local/etc/macports/sources.conf
# Add this line ABOVE the "rsync://...  [default]" line
# (please change "yourname" as your username)
file:///Users/yourname/git/JojojolPorts/overrides
% sudo chmod a-w /opt/local/etc/macports/sources.conf
% cd ~/git/JojojolPorts/overrides
% portindex
```
Confirm it took effect - the description should mention the override, not the plain upstream one:
```sh
% port info cmake-bootstrap
```

### Install py-optuna (2.10.0) by MacPorts
```sh
% sudo port install py38-optuna
```
or
```sh
% sudo port upgrade py38-optuna
```
