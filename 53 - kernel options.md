mdadm, raid0/1/456/10, vfat, btrfs, etc.
Enable bpf() syscall
Auditing support
Enable system-call auditing support
Harden SLAB freelist metadata
SLAB freelist randomization
Control Group Support
Namespaces Support
Preemption Model
Networking/netfilter enable bpfilter
  ./config:
	CONFIG_INPUT_MOUSEDEV
	CONFIG_RAID_ATTRS=y
	CONFIG_CGROUP_DEVICE
	CONFIG_USER_NS
	CONFIG_VETH
	CONFIG_TUN
	CONFIG_MACVLAN
	CONFIG_BONDING
	CONFIG_BRIDGE
	CHECKPOINT_RESTORE
	UNIX_DIAG
	INET_DIAG
	INET_UDP_DIAG
	PACKET_DIAG
	NETLINK_DIAG
	NETFILTER_XT_MATCH_COMMENT (Networking Support -> Networking Options -> Network packet filtering framework -> (Advanced Config = *), Core netfilter config -> netfilter xtables support)