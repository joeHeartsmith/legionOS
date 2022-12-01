**system/critical** (base)
	linux (PATCH: standard compilation options) (PATCH: ipx)
	*firmware*
	ld
	initramfs-tools
	*os-prober (maybe just in installer)*
	*pciutils*
	grub2 (*spaceballs: the bootloader*)
	efibootmgr
	os-core-pak (stage0)
	multi-lib-native
	libc
	btrfs-progs
	e2fs-progs
	dosfstools
	mkswap
	mdadm
	fsck
	(init system)
	busybox
	coreutils
	chroot
	dmsetup	
	udev
	mount
	console-setup
	login
	kmod
	util-linux
	*(klibc-utils) (if necessary)*
	*procps*
	*(PAM)
	selinux*
	*auditd*
	*dmidecode*
	*dkms*
	cron
	syslog
	*logrotate*
	*ncurses*
	wine/proton
	*anbox/waydroid*
	*darling*
	
**system/support**
	ca-certificates
	geoip-database
	ip-service (/etc/service)
	dns-tld (list of tlds)
	manpages (+man-db)
	openssl/libressel
	tzdata
	(firmware)
	man/man-db
	syslog
	
**system/utility**
	(package manager)
	(fsprogs)
	(disk SMART utils)
	(fan/temp utils)
	dpkg
	rpm
	*fdisk*
	parted
	cpuid
	*hdparm*
	*eject*
	*usbutils*
	adduser
	passwd
	*diffutils*
	*discover*
	rsync
	isc-dhcp-client
	chronyd/ntp-client
	iproute2
	iptables
	iptables-persist
	inetutils
	hostname
	*bind9-host*
	net-tools (PATCH: appletalk ddp)
	ifenslave
	ipx-tools
	*netatalk*-2.2.6 (PATCH: linux/BSD socket issue) (also, disable service by-default)
	atalk-tools
	openssh-client
	openssh-server
	telnet
	lsof
	sudo
	*gettext*
	*readline*
	*rpm
	rpm2cpio*

**shell**
	dash	
	bash
	*zsh*
	
**editor**
	vi
	vim
	nano
	*emacs*

**user/utility**
	file
	grep
	sed
	*groff*
	tr
	awk
	patch
	links
	whiptail
	*most*
	less
	binutils
	bsdutils
	tar	
	gzip
	*bzip2*
	xz-utils
	*cpio*
	*unzip*
	findutils
	*mlocate*
	*gnupg*
	netcat
	*tcpdump*
	*traceroute*
	*wget*
	curl
	shellcheck
	*winnt-nativeapp-helper*

**dev**
	(dev-tools-all)
	git
	*xxd*
	
**library**
	ld
	elf
	glibc
	*SDL/SDL2*
	crypt
	curses
	gthread
	ncurses
	pthread
	*resolv*
	*sepol*
	ssl
	udev
	util
	z
	