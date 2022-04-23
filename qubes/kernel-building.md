<h1>Qubes Kernel Building</h1>

Clone debian11 template, d11-kernel.

In d11-kernel:  
`sudo apt install build-essential linux-source bc kmod cpio flex libncurses5-dev libelf-dev libssl-dev rsync python3 bison e2fsprogs`


On Wed, May 18, 2016 at 09:03:43AM -0700, Holger Levsen wrote:

I'm still pondering doing the same, and looking at the cubes git repos I've identified these as being needed for dom0:

qubes-core-admin
qubes-core-admin-linux
qubes-core-agent-linux
qubes-core-libvirt
qubes-core-vchan-xen
Is that correct? Which are missing?

In addition to above:

qubes-vmm-xen (yes, you need this, not native Debian packages because
of Qubes-specific patches, and parts in Debian packages - libxenvchan,
stubdomains)
qubes-gui-common (required to build gui-daemon)
qubes-gui-daemon
qubes-core-qubesdb
qubes-manager
And mgmt-salt stuff (everything with "base" and "dom0").

Some of them already have debian packaging.

Packaging Xen for dom0 would be tricky because of stubdomains. It
consists of some external libraries/tools built as part of Xen build and
statically linked. Something that AFAIR is against Debian policy (for
example there are multiple source tarballs, from different projects).

And template packages needs to be converted to deb. Or not packaged at
all and installed some other way - which I think would be even better
option (installing templates as packages have a lot of side effects...).

Cause once dom0 is working one should be able to deploy VMs from a backup… ;-)

Yes, it should be possible.
