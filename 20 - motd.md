information to dynamically populate motd (kind of like ubuntu server)
  !  this should not be more than ~5 lines, and *should be easily disabled*

- current date, time, timezone
- system status
	- hostname fqdn
	- uptime
	- easy-to-read CPU, disk I/O, network load
	- last login (ip, user, time)
		- add geo info based on IP?
- issues from [[60 - fs-boot-watchdog]] and [[61 - package-service-watchdog]]
- special security updates & git package blacklist notifications
- output from `curl -s wttr.in`?
- `fortune | cowsay | lolcat`, except the fortunes are useful system admin notes for the distro