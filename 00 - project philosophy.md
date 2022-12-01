- a simple, small, baseline distro with minimal/no learning curve for advanced users (think the flexibilty and power of gentoo or slack, with the simplicity and reliablity of debian, mixed with the things I do to make my life easier, and some extra sprinkles on top)
	- quick install must be an option
	- good as baseline for standard servers/lightweight desktop environments
		- or also for hosting VMs + containers
	- does (almost) nothing for you, makes (almost) no assumptions (but still has a 'personality';  no linux distro can be truly agnostic, but here we try to provide a highly-compliant POSIX.2 + SUS baseline, with some convenience tools that merely serve as the frosting on the cake)
	- high-security (or at least as much as the user selects during install)
		- cutting-edge package versions are preferred (but of course, overrideable; we would prefer services to crash because they are unstable, not because they are vulnerable)
	- high-performance (decent tunes built-in for fast networking, I/O, and service responsiveness)
	- more cuttinaims for stability when security posture allows, and tries to fill the gaps in stability manually when possible (quality ports, kernel live patching (ksplice), limit base install to secure packages + configurations)
		- maybe also offer something like that for services (i.e. when a package is upgraded, do a test-install in a container, or alt-namespace, and if the service fails to start, don't install it, and just notify the user instead)

- small footprint, fast (if using binary packages) installer
	- gentoo-like metadistribution (no installer disc necessary, just a 'stage3', and we can easily pull cedalion from the web, and start an install from anywhere)
	- but should create a simple mechanism to build new install media (i.e. just run a makefile to build the whole distro)
		- when combined with some git automation for the package manager, the entire distro should be relatively low-maintenance to maintain
		- this also allows for full customization in a very easy way
		- and allows for easy rolling releases

- offers some native utilities (i.e. [[69 - winnt-nativeapp-helper]], or [[60 - fs-boot-watchdog]]), and the config utilities will use curses-based UIs (so that a DE is never necessary)

- 'scripts' based config system ([[02 - scripts system]])
	- common services (especially boot configs) should just be run as executable scripts (instead of config files that you have to research (and that may not be exhaustive in capability)

- agnostic(-ish) packaging (git-based package manager for core, augmented by BSD ports collection)
	- use Joyent's binary packages for Linux (https://pkgsrc.joyent.com/install-on-linux/)
	- 'patches' system (i.e. patches for programs in *this* distro) ([[03 - patches system]])
	- package manager is just a wrapper around the ports/pkgsrc system so that modifications can be made on-the-fly (i.e. customization prompts during install, or the [[03 - patches system]] can be leveraged)

- broad compatibilitiy (i.e. standard libc, POSIX/SUS compliance)
	- systemd/openrc??

- POSIX/SUS baseline environment (minimum tools)
	- but also subtle additions (like ipx-tools for ready-compatbility + usage)

- E-Z multiarch support (qemu-user-static + binfmt_misc out-of-the-box)
	- makes it easy for devs (and users) to 'just run' binaries from foreign architectures


- *PROJECT NAME:* because this is based on putting together some of the personalities of other distros, something in mythology relating to multiple-personalities
	- legion (as in the collection of demons in the bible)
		- this will be the distro name
	- sielu (finnish for 'soul', where the uralic belief is that souls have multiple parts to be complete)
		- this will be the name for the package manager (because package management systems tend to form the 'soul' of a distro)
	- cedalion (stood on orion's shoulder; i.e. 'standing on the sholders of giants', in line with the theme of this work)
		- this will be the name for the distro installer (and configuration tool)