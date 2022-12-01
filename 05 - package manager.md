- name:
	- sielu pkg manager (spm) (?)
	- package keeper - git (pkg) (?)

- should wrap around ports/pkgsrc system
	- the actual package manager should be a wrapper for everything, maintaining its own database
	- this allows for easy modification (PATCHES)/during-install configuration/USE-flags style options
		- USE-flags should be in the manifest (i.e. how the build steps change based on the desired configuration)
	- also, what about monolithic programs (i.e. flatpaks, snaps, and appimages)?

- should work with COW filesystems automatically (configureable, but by default, snapshot-before-update)
	- should also know how to clean the snapshots it generates (i.e. package manager snapshots should be marked uniquely, and should be deleted after a set amount of time/storage usage, as long as there are no branches from those snapshots)

- thanks to [[62 - multi-lib]], all packages should be available in multiple architectures
	- the preferred architecture should be specified in the sielu configuration file (and should be set/modified by cedalion)
	- this should be overrideable during package download (i.e. `spm install busybox --arch=i686` will pull-down the 32-bit version of busybox (*and its library dependancies in the matching arch*) regardless of the system)
		- in cases like this, there should be a virtual dependency (based on the architecture name, not what's in the manifest). if the user doesn't have the *multi-lib-ARCH* that they need, they will be warned that the package will fail until they install it.
	- the git server should create branches for each build (i.e. busybox-1.35_amd64 vs busybox-1.35_i686 to get the binaries)
	- also, because of this, the package manager needs to be able to inform the repo server what native CPU ISA it has
		- this way, packages like *multi-lib-native* can work, because spm will inform the repo that it's running i.e. on *amd64*, and the *multi-lib-native* MANIFEST can specify a RUNTIME-DEPENDS of *multi-lib-amd64* when the *arch:amd64* requisite is satisfied

- git-based package management system
	- i.e. 'pkg install net-tools' would just download, build, and install net-tools from github (or smaklab.com's git server, or gitlab, or whatever the user's got configured)
	- great for community development, because you can just clone stock repos and modify them to your liking.  if they work, you can just point your package manager at somebody else's repo (i mean there's definitely some security risk here, but a notice should suffice)
	- obviously makes source-level modifications easy; users can just pull the packages (i.e. `--download-only`), and then the package manager can just drop them in the directory of the newly-downloaded package
		- once the user finishes modifying the source, the package manager can just pick up where it left off (i.e. make/install)
			- the package manager will need to know how to recover from source file errors
		- in order to avoid (or enforce) extra build time, the user can leave the binaries intact (i.e. `--no-make-clean`)
	- requires description file in each repo for dependencies, required build tools, and build directions, and binary package location url
	- start with a small github account, forking packages that are essential to build the system
		- as packages are attempted to be downloaded, the ones that the repo don't have should be recorded, and the top-ranking missing packages should be added to the repo
	- repos with only a manifest are equivalent to metapackages
	- updates are now simply git synchronizations; if there are changes, re-build and re-install
	- package manager config for 'repos' would simply be which github/gitlab/etc accounts to search packages from, in ranked order
	- manifest contents: (with optional version requirement)
		- VERSION-RANGE (there may be multiple version-range segments, because things can change as software projects grow)
		- BUILD-DEPENDS (requirements to actually produce binaries)
		- RUNTIME-DEPENDS (i.e. libraries and helper software)
			- These should have configurable *requisites* that can be satisfied based on the install.  For example, there could be an open-block for *arch*.  Under that, there could be an open-block for *amd64*, and under that, there could be an open-block for *pkg-depend*, where something like *multi-lib-amd64* would be listed.
				- this is going to push the config file complexity requirements to a place where we'll need to create a genuine parser.  for now, we should probably just write the MANIFEST files in JSON, so that a quick-n-dirty spm beta release can use native Python libs to parse it out.
			- BUILD-INSTRUCTIONS (i.e. 'configure; make; make install)
		- PACKAGE-OPTIONS (these are the types of things that will require user intervention, for example, which architectures the user wants when installing [[62 - multi-lib]])
	- package manager should also be able to locate & install github packages as well
	- this package manager could be the combo answer to both systems (i.e. if git repos are mirrored into this distro's git user page so the manifest may be included, it follows that the binary package could also be included.  then, you can use a singular package management front-end to get source (like ports), or packages.  the whole thing could still work with pkgsrc, as well)
	- fallback behavior required for packages ('repos') that don't have a manifest
		- probably ask for user intervention
		- if all else fails, just exit with an error, and let the user know that once they successfully build the package, they can inform the package manager with a command to update its database
	- packages may not work after updates sometimes, so we'll need a mechanism to blacklist certain versions (and of course, a method for users to override that)

- There should be a (by default) *HIGHLY-AGGRESSIVE* update mode, where the package manager and the repo work together to try to push packages ASAP (i.e. as soon as a maintainer/developer commits an update to the MASTER branch, the repo git server synchronizes it and buils it, and pushes notifications to the distros that there is an update to be had.  Ideally, Legion users should be able to automatically upgrade to the latest version of a piece of software within minutes).
	- In opposition to this, there should be a *STABLE* mode that attempts to maintain all the packages in the system to that of the version manifest for whatever distro release you have set (i.e. bleeding, latest-tested, stable-rolling, stable-longterm, static)

- for the git system, the local git repo for the distribution should periodically check for repo updates, make-clean, rebuild, and git-commit the new binaries in there
	- then, an entire distribution can simply be described as a list of preferred package versions to the package manager during install/update
		- we can define various profiles in this manifest
			- BLEEDING: the absolute latest release.  as soon as a repo maintainer pushes a commit, we sync on it ASAP
			- LATEST-TESTED: somewhere around BLEEDING, but not until packages have seen some usage, and there are no (or limited) reports from package managers that there are issues
			- STABLE-ROLLING: the regular distro profile for more formal installation scenarios.  all packages here should have a >90% success rate report
			- STABLE-LONGTERM: same, but less commits should be made to this for a well-defined period of time (i.e. 6 months or a year).  all packages should have a >99% success rate
			- STATIC: no manifest is used, so no updates.  a system was built this way, and all updates will be manually managed by the user.  dependencies can still be pulled when getting packages.
		- also, if there's an automated build system, it can commit the latest version of a working build, and commit that info into these long package/version tuple lists
	- ...or, users can do the rolling release thing, and just update all the time
	- ...and the git server can also host a simple http service that shows the date that any package repos have been updated (this way package update checks can quickly end if there's nothing to do)

- all repos should be accessed for updates and handshakes via HTTPS, so that domain verification can take place via TLS certs
	- this way, we don't have to worry about a separate key-management system for authentication
	- the package manager should (without a '--no-auth-warn' style option) throw a loud warning when not using SSL