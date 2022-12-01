- name: cedalion (stood on orion's shoulder; i.e. 'standing on the sholders of giants', in line with the theme of this project, but cedalion was also a guide for orion, like the installer guides the user/distro)

- also the global system configuration tool (not as far as something like YaST (we're not configuring individual services with this tool), but at least you can run cedalion from an existing system i.e. to repair/refresh an installation, or start it from an existing installation to repair/refresh it)
	- does things like global permissions repair (DAC + MAC), and mass package re-installation (like a system refresh)
		- thanks to btrfs-by-default, we can also just diverge the system into a new snapshot branch (and destroy the new branch if things don't work out, or destroy the old one to save space)
	- if running from installation media, just jump to new installation mode
	- if not, you can just let the user specify the location of a Legion install, and let cedalion chroot into it + configure it

- cedalion should easily be able to create custom containers/VMs for services (instead of chrooting into a disk partition, just chroot into a bind-mount or disk image, and then start it with QEMU-KVM or lxc/docker)

- web-based application.  you should just be able to browse to something like smaklab.com/legion/cedalion, and install/configure your system via client-side scripting (probably use JS to download/execute heavy-lifting python scripts; the initial python script should privesc, and download/spawn the rest of the scripts, so that the browser doesn't have to be run as root, and password is only asked once)
	- the install media should present this server locally (especially when web access might not yet be accessible)
	- this is cool, becuase you can just browse to this location from anywhere (like KNOPPIX) and install your system
	- internationalization becomes easy here too, because we can just use https://github.com/joeJamison/tranlang to detect the user's locale for website content presentation (*and also package selection*)
	- portability is the same, because you can pull it (hopefully) from the user-agent string

- Initial Installer Behavior (i.e. from installation media)
	- start GNU screen locally
		- put things like ip address, time, and ssh login info into the hardstatus line
	- start web services ASAP (sshd, installer local web service)
	- installation music (piano, muted by default, speaker icon in corner)
	- present a web site (this works if KNOPPIX is our 'installer disc')
		- if using a barebones livecd, just start links (perferrably links 2 w/framebuffer gfx, or at least links 1 w/colors enabled)
	- basically just a big form with every question (some fields are mandatory)
		- most fields should be filled-in with default values
		- this way, the user only needs to click 'OK'
			- pedantic stuff like locale, console font (with image previews), etc
		- offer a chance to disable the few default features available (i.e. auditd)
	- asks things ahead-of-time (like preferred security posture)
	- btrfs by-default
		- w/fs-boot-watchdog
	- pre-populates 'scripts' system (and shows output, allowing users to change before first boot)
	- sets up:
		- users
		- hostname
		- hosts file
		- fstab (pretty)
		- DNS
		- NTP
		- terminals (including serial terminals, on by default)
		- consolefont
		- users + passwords
		- initial services (just ssh, asks for listen-port + bind-address, offers to upload/download key-certs)
		- openRC/init config
		- other critical configs in /etc/
	- install [[62 - multi-lib]] and ask for initial desired libraries (probably just amd64, i686, and arm64 as default selections)

- creates initial system snapshot on initial boot with btrfs

- post-installation actions
	- set a one-time MOTD that, at a minimum, mentions the following:
		- thank you
		- installation details (release version, package manager profile, architecture, etc)
		- website documentation address
		- package manager name
		- show documentation links for the the software that is unique to this distro (i.e. fs-boot-watchdog, cedalion, sielu, etc)