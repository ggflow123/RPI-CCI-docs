# Visual Studio Code on RPI CCI

This instructions is about how to use Visual Studio Code as an edit to modify files on RPI CCI.

While RPI has documentation on using[ sshfs for mounting](https://docs.cci.rpi.edu/examples/Advanced_SSH/#remote-filesystem-mounting), I also include necessary instructions and links, especially for Mac OS users.

## Step 1: Install sshfs

For **Linux** and **Windows Subsystem for Linux (WSL),** do

```
sudo apt-get install sshfs
```

For **Mac,** feel free to check and follow this [link](https://www.petergirnus.com/blog/how-to-use-sshfs-on-macos). The steps of installation are:

1. Install [macFUSE](https://osxfuse.github.io). While installing macFUSE, need to allow **[third party kernel extensions](https://github.com/macfuse/macfuse/wiki/Getting-Started#enabling-support-for-third-party-kernel-extensions-apple-silicon-macs).**
2. After finishing installing macFUSE, install [SSHFS](https://osxfuse.github.io).

## Step 2: Mount

### 1. Main Directory

Setup a main directory on local computer to store contain all of our mount point:

```
mkdir ~/mounts
cd ~/mounts
mkdir home
```

### 2. Connect with SSHFS

With SSHFS installed, create an connection to RPI CCI. The usage pattern is:

```
sshfs <USERNAME>@<HOSTNAME>:/path/to/desired/directory /path/to/mount/point -o <OPTIONS>
```

A typical example is:

```
sshfs EXPLname@blp01.ccni.rpi.edu:/gpfs/u/home/EXPL/EXPLname ~/mounts/home -o follow_symlinks
```

-o follow_symlinks is necessary because the home directory on CCI has barn, barn-shared, scratch and scratch-shared. Without symlinks, these shortcuts will remain blank. Refer to the same RPI[docs](https://docs.cci.rpi.edu/examples/Advanced_SSH/#remote-filesystem-mounting) for more details.

To unmount in terminal, do:

```
sudo umount ~/mounts/home
```

If the above command is not working, reboot the system will do the trick.

On **Mac using macFUSE,** SSHFS essential works like an external disk. Directly eject the external mounting disk will unmount automatically.

## Reference:

[RPI CCI DOCS](https://docs.cci.rpi.edu/examples/Advanced_SSH/#remote-filesystem-mounting)

[https://www.petergirnus.com/blog/how-to-use-sshfs-on-macos](https://www.petergirnus.com/blog/how-to-use-sshfs-on-macos)

[https://github.com/macfuse/macfuse/wiki/Getting-Started#enabling-support-for-third-party-kernel-extensions-apple-silicon-macs](https://github.com/macfuse/macfuse/wiki/Getting-Started#enabling-support-for-third-party-kernel-extensions-apple-silicon-macs)
