---
title: Installing
---

# Foreword: "Where's the app for (insert my OS here)?"

[GTG](index) is an application made and tested on Linux-based OSes
(like [Fedora](https://getfedora.org) and [Ubuntu](https://ubuntu.com)).
Some rumors say it works on \*BSD, but we're pretty sure it does *not*
work on Windows (because none of us run that). We're developing GTG to
make our lives more pleasant and productive on Linux, not to compete
with the plethora of proprietary GTD apps out there.

"Do one thing and do it well" means we can only commit to supporting the
Linux platform, and only through [Flatpak](https://flatpak.org/)
packages. Life is too short to maintain a gazillion ports on a bunch of
other platforms (Windows/macOS/Android/iOS/Hurd) without compensation.
If you want to join the project to contribute and maintain a port to
other platforms however, you are more than welcome to do so!

# Installing Getting Things GNOME on Linux

## If you want it to Just Work™

### Official Flatpak packages

![](https://flatpak.org/img/delivery_truck2-bb72338f.png "Delivery truck with Flatpak on it")

We are providing Flatpack packages, which are the emerging standard.
Flatpak packages made by the GTG Team are considered the recommended way
to install (and test) GTG.

Our Flatpak package is for the latest stable GTG release, and is
[available on Flathub](https://flathub.org/apps/details/org.gnome.GTG).

Due to our limited resources, flatpaks are the only packages we will
officially support (we will not make "PPA" or "COPR" package
repositories, and if you are reporting bugs, please make sure to test
that the bug is reproducible in our Flatpak version, and preferrably in
the development/Git version as well).

You are, of course, welcome to run the development version from Git (for
testing and contributing) using our traditional "launch.sh" script, to
see bleeding edge technology in the making. See the "requirements and
instructions for manual installs" further below on this page.

### Linux distributions providing GTG

First, make sure¹ that your Linux distribution provides the latest
version of GTG, as seen on our [list of downloadable releases](https://github.com/getting-things-gnome/gtg/releases) and in
our [history of GTG releases](release_names). We cannot
support outdated releases.

Various distributions (Fedora, Ubuntu, Debian, OpenSuSE, Arch, Gentoo,
OpenBSD, FreeBSD) used to package GTG, but as of 2019 most had stopped.
If your distro has started packaging GTG again (version 0.6 and above),
feel free to let us know or to update this page.

New list of distros that have packages¹ for GTG as of 2023:

- Arch Linux: [AUR package of the Git version of GTG](https://aur.archlinux.org/packages/gtg-git/)
- Gentoo: [Gentoo package for the stable version of GTG](https://packages.gentoo.org/packages/app-office/gtg)
- OpenSUSE Tumbleweed & Leap: [Package for the stable version of GTG](https://software.opensuse.org/package/gtg)
- Debian: [Debian GTG package](https://tracker.debian.org/pkg/gtg)²
- Ubuntu: [Ubuntu GTG package](https://packages.ubuntu.com/lunar/gtg)²
- Potentially upcoming:
  - Fedora: the package had previously been retired, and would
    require someone to step forward as a packager and go through the
    "un-retirement" process (details
    [here](https://bugzilla.redhat.com/show_bug.cgi?id=1573480#c9)).
    Please be that someone! 2021-10 update: it seems someone is now
    [working](https://github.com/getting-things-gnome/gtg/issues/709)
    on reintroducing GTG into Fedora.

Important notes:

¹: Remember that we do not make the distro packages ourselves. The only
thing that most code maintainers systematically test and run is the
source code and the Flatpak package we maintain on Flathub.

²: Please be aware that Debian and Ubuntu LTS have a reputation for
having excruciatingly long release lifecycles and typically provide very
outdated packages. Before reporting bugs upstream in GTG, always check
if the version provided by your distro matches the version we provide as
a Flatpak via Flathub (and if that isn't the case, test with the Flatpak
version).

## Requirements and instructions for manual installs

Check out our
[README](https://github.com/getting-things-gnome/gtg/blob/master/README.md)
for the list of dependencies and how to solve them.

This is particularly useful for potential contributors and testers
interested in the latest development version. In that scenario, you can
simply run "gtg.sh" and not worry about affecting the rest of your
system.

If however, you're the kind of person to install system-wide from
source/tarballs, you will know where to find them. The instructions are
mostly the same, see the
[README](https://github.com/getting-things-gnome/gtg/blob/master/README.md)
file for some tips. When you want to install GTG on your system
system-wide, you can use the traditional setup.py... but unless you
*really* know what you're doing, we would highly recommend you use our
Flatpak packages instead.

# Windows

Note that there was an attempt at porting to Windows, aeons ago, with no
installer. See [Gettings Things Gnome! Windows on Launchpad](https://launchpad.net/gtg-win) if you're interested in
archeology or would like to resurrect that effort for the current
codebase.
