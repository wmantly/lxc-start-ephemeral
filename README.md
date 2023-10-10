## Hack for 'lxc-start-ephemeral`

I wrote this insanity to get back the functionality of `lxc-start-ephemeral` from LXC v2. 
"But what about `lxc-copy -e`"... well, it does work BUT it has one major issue I could not get around.
If you ephemeral clone a debian bases distro, and try to run `apt get install <anythin>`, you ALWAYS
get this error message:

```bash
Reading package lists...
Building dependency tree...
Reading state information...
The following NEW packages will be installed:
  xe
0 upgraded, 1 newly installed, 0 to remove and 8 not upgraded.
Need to get 13.7 kB of archives.
After this operation, 47.1 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu focal/universe amd64 xe amd64 0.11-4 [13.7 kB]
debconf: unable to initialize frontend: Dialog
debconf: (TERM is not set, so the dialog frontend is not usable.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (This frontend requires a controlling tty.)
debconf: falling back to frontend: Teletype
dpkg-preconfigure: unable to re-open stdin: 
Fetched 13.7 kB in 0s (191 kB/s)
Selecting previously unselected package xe.
(Reading database ... 31539 files and directories currently installed.)
Preparing to unpack .../archives/xe_0.11-4_amd64.deb ...
Unpacking xe (0.11-4) ...
dpkg: error processing archive /var/cache/apt/archives/xe_0.11-4_amd64.deb (--unpack):
 unable to install new version of './usr/share/doc/xe': Invalid cross-device link
Errors were encountered while processing:
 /var/cache/apt/archives/xe_0.11-4_amd64.deb
E: Sub-process /usr/bin/dpkg returned an error code (1)
```

This is no good for how I needed to use ephemeral LXC. My "hack" is based on the LXC v2
pre-mount hook that would be found in ephemeral containers.

If for any reason you need to do this, please edit the files as all of them are hard coded for the `virt` user.
Everything can be `chmod +x` and places in `/usr/loca/bin` execpt for the suders file. If you have made it here,
I hope you know what to do with the sudoers file.
