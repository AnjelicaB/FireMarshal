FireMarshal
==================================

This tool builds base images for several linux-based distros that work with qemu,
spike, and FireSim.

This is just a quick primer. To see full documentation, please see the official
documentation:
https://firemarshal.readthedocs.io/en/latest/index.html

# Requirements
The easiest way to use Marshal is to run it via Chipyard
(https://chipyard.readthedocs.io/en/latest/) or FireSim
(https://docs.fires.im/en/latest/). However, this is not required. 

To run FireMarshal, you will need the following dependencies:

## Standard Packages
``centos-requirements.txt`` is a list of packages for centos7 that are needed by
marshal. You can install these with:
```
cat centos-requirements.txt | sudo xargs yum install -y
```

``ubuntu-requirements.txt`` is a list of packages for Ubuntu 18.04 that are needed by marshal.
You can install these with:
```
cat ubuntu-requirements.txt | sudo xargs apt-get install -y
```

Package names may be different on other distributions.

### Note for Ubuntu
The libguestfs-tools package (needed for the guestmount command) does not work
out of the box on Ubuntu. See
https://github.com/firesim/firesim-software/issues/30 for a workaround.

## Python
This project was written for python 3.8. You can install all dependencies using:
```
pip3 install -r python-requirements.txt
```

## Other Packages
FireMarshal depends on other open-source packages that can be installed by running:

```
./marshal-dependencies.sh
```

Note that this script downloads dependencies to a `dependencies` directory and installs them at the path pointed to by the `RISCV` environment variable. Thus, the script requires `RISCV` to be set (Chipyard/FireSim already do this).

This script also updates submodules.

## RISC-V Tools
In addition to standard libraries, you will need a RISC-V compatible toolchain,
the RISC-V isa simulator (spike). This is already installed by Chipyard/FireSim.

See the [Chipyard documentation](https://chipyard.readthedocs.io/en/latest/Chipyard-Basics/Initial-Repo-Setup.html#building-a-toolchain)
for help setting up a known-good toolchain and environment.

## Qemu
Qemu is the default simulator used by FireMarshal and it currently installs v6.2.0.

# Basic Usage

Building workloads:

    ./marshal build br-base.json

To run in qemu:

    ./marshal launch br-base.json

To install into FireSim (assuming you cloned this as a submodule of FireSim or Chipyard):

    ./marshal install br-base.json

# Security Note
Be advised that FireMarshal will run initialization scripts provided by
workloads. These scripts will have all the permissions your user has, be sure
to read all workloads carefully before building them.

# Getting Help / Discussion:
* For general questions, help, and discussion: use the FireSim user forum: https://groups.google.com/forum/#!forum/firesim
* For bugs and feature requests: use the github issue tracker: https://github.com/firesim/FireMarshal/issues
* See CONTRIBUTING.md for more details
