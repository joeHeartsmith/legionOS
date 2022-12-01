- replace *custom* config files w/scripts
	- (i.e. instead of /etc/network/interfaces, just have init run the executable scripts in /etc/network/)
	- importantly, these scripts need to be easy-to-find by-name, in common locations

- mostly applies to init-scripted events
	- network interfaces
	- firewall (speaking of which, should ip6tables automatically add protective rules (based on prompt during installation)?)
	- console getty/RS-232 setup
	- generic user 'runme' startup script

- also should be easily built for custom boot scripts
	- called from init after everything else is done

- the default scripts provided by the installer should be *shellchecked*
