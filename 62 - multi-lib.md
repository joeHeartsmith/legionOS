package for getting libraries for multiple architectures onto the same root

- should also check the local CPU architecture, and if the requested library set cannot be executed by that CPU, bring in the applicable qemu-user emulator, and configure binfmt-support to execute binaries from that architecture

- there should be a package for each arch (i.e. *multi-lib-amd64*)
- *multi-lib-native* is the metapackage that just figures out which architecture you have, and downloads it (i.e. fetching *multi-lib-native* on an ARM64 machine will get the *multi-lib-aarch64* package)
