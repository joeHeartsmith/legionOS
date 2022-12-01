- a small utility used to quickly deploy a (highly-accelerated) QEMU-KVM windows VM (curses-based)
	- offers initial setup:
		- pulls a windows ISO from the Legion site that's got a deployment script already setup
		- gets product key from user (or doesn't)
		- patches terminal services binaries (pulls from Legion site)
		- configures RemoteApp
		- offers to start headless VM as boot service
		- VM network configuration
			- NAT vs bridge
			- if bridging is selected, print the applicable code needed to add to the network setup SCRIPT)
			- if local-access-only is selected, print different applicable code to add the the network setup SCRIPT, but without bridging)
	- once installed, allows users to build + deploy RemoteApp shortcuts to their local machine

- *DEPENDANCY*: spice-qxl (?)