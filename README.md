MSYS2-packages
==============
[![TeaCI status](https://tea-ci.org/api/badges/Alexpux/MSYS2-packages/status.svg)](https://tea-ci.org/Alexpux/MSYS2-packages)
[![AppVeyor status](https://ci.appveyor.com/api/projects/status/github/Alexpux/MSYS2-packages?branch=master&svg=true)](https://ci.appveyor.com/project/Alexpux/MSYS2-packages)

Package scripts for MSYS2.

To build these, run msys2_shell.cmd then from the bash prompt. Packages from
the msys2-devel and base-devel groups are implicit build time dependencies.
Make sure both are installed before attempting to build any package:

    pacman -S --needed base-devel msys2-devel
    cd ${package-name}
    makepkg

To install the built package(s).

    pacman -U ${package-name}*.pkg.tar.xz

## hacking

install git sdk, then:

```bash
git checkout msys2-runtime-2.x
vim /etc/pacman.conf # SigLevel -> Never
pacman -Syy
sdk init MSYS2-runtime # broken - because of master branch rename to main (yay for political correctness...)

# walkaround
cd /usr/src/MSYS2-packages
git fetch
git checkout main
git checkout -b master
sdk init MSYS2-runtime
# end of walkaround

cd /usr/src/MSYS2-packages/coreutils
git remote set-url origin git@github.com:ptixed/MSYS2-packages.git
git fetch
# git rebase # first check how does local copy differ from remote
makepkg -s
```

to run programs from pkg/ you will also need /usr/bin/msys-2.0.dll

