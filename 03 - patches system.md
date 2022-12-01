provide localized patches for ports on this distro
  make the package manager a wrapper around ports/pkgadd so that patches can be made
    this can also give you eselect/USE-flags type functionality (sort of, the git manifest system should do this as well when it configures the build environment)

- patch sets should be kept in a gitignored tarball
	- one diffpatch file per version

- patches:
	- standard kernel options (i.e. btrfs, selinux, hardening options, etc) (find gentoo install notes for the whole list)
	- netatalk (socket/bind issue)
	- net-tools (appletalk ddp /proc issue)
