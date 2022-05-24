# BSD-Bootcode-Updater

 FreeBSD Bootcode Updater Utility (**Experimental**)
 
 This is an attempt to make an easy to use FreeBSD bootcode updater utility for GPT/BIOS and EFI system boot.
 
 
 ## CLI Options
 
 ```
 root@mserver: ~# bootcode-update -h
Usage: bootcode-update [option]
Options:
        -d | --dryrun   Execute a dryrun test only.
        -e | --efi      Update EFI bootcode.
        -g | --gpt      Update GPT/ZFS bootcode.
        -a | --all      Update both EFI and GPT bootcode.
        -h | --help     Print this help message and exit.
        -v | --version  Print the version info and exit.

 ```

# Examples

**Updating bootcode in a RootOnZFS Mirror setup with GPT-BIOS + UEFI boot(BSD12.x):**
 ```
 root@mserver: ~# uname -r
12.3-RELEASE-p5
root@mserver: ~# bootcode-update -a

UEFI Partition: [ ada0p1 ]
Disk Serial:    [ XXX519GYXXXXXX ]
Proceed with EFI bootcode update for the following geom: [ada0p1] (Y/n)?: y
Proceeding...
=> Updating EFI bootcode on ada0p1
/boot/loader.efi -> /tmp/boot_esp/efi/boot/bootx64.efi
=> Success!


UEFI Partition: [ ada1p1 ]
Disk Serial:    [ XXX817TM85A3TDXXXXXX ]
Proceed with EFI bootcode update for the following geom: [ada1p1] (Y/n)?: y
Proceeding...
=> Updating EFI bootcode on ada1p1
/boot/loader.efi -> /tmp/boot_esp/efi/boot/bootx64.efi
=> Success!


Boot Partition: [ ada0p2 ]
Disk Serial:    [ XXX519GYXXXXXX ]
Pool Member:    [ zroot: '/dev/ada0p4' ]
Proceed with GPT/ZFS bootcode update for the following geom: [ada0p2] (Y/n)?: y
Proceeding...
=> Updating GPT/ZFS bootcode on ada0p2
partcode written to ada0p2
bootcode written to ada0
=> Success!


Boot Partition: [ ada1p2 ]
Disk Serial:    [ XXX817TM85A3TDXXXXXX ]
Pool Member:    [ zroot: '/dev/ada1p4' ]
Proceed with GPT/ZFS bootcode update for the following geom: [ada1p2] (Y/n)?: y
Proceeding...
=> Updating GPT/ZFS bootcode on ada1p2
partcode written to ada1p2
bootcode written to ada1
=> Success!
 ```

**Updating bootcode in a RootOnZFS Mirror setup with GPT-BIOS + UEFI boot(BSD13.x):**
 ```
 root@freebsd13vm:~ # uname -r
13.1-RELEASE
root@freebsd13vm:~ # bootcode-update -a

UEFI Partition: [ ada0p1 ]
Disk Serial:    [ VB1e797887-f29c3a29 ]
Proceed with EFI bootcode update for the following geom: [ada0p1] (Y/n)?: y
Proceeding...
=> Updating EFI bootcode on ada0p1
/boot/loader.efi -> /boot/efi/efi/boot/bootx64.efi
/boot/loader.efi -> /boot/efi/efi/freebsd/loader.efi
=> Success!


UEFI Partition: [ ada1p1 ]
Disk Serial:    [ VBc718718d-961de995 ]
Proceed with EFI bootcode update for the following geom: [ada1p1] (Y/n)?: y
Proceeding...
=> Updating EFI bootcode on ada1p1
/boot/loader.efi -> /tmp/boot_esp/efi/boot/bootx64.efi
/boot/loader.efi -> /tmp/boot_esp/efi/freebsd/loader.efi
=> Success!


Boot Partition: [ ada0p2 ]
Disk Serial:    [ VB1e797887-f29c3a29 ]
Pool Member:    [ zroot: '/dev/ada0p4' ]
Proceed with GPT/ZFS bootcode update for the following geom: [ada0p2] (Y/n)?: y
Proceeding...
=> Updating GPT/ZFS bootcode on ada0p2
partcode written to ada0p2
bootcode written to ada0
=> Success!


Boot Partition: [ ada1p2 ]
Disk Serial:    [ VBc718718d-961de995 ]
Pool Member:    [ zroot: '/dev/ada1p4' ]
Proceed with GPT/ZFS bootcode update for the following geom: [ada1p2] (Y/n)?: y
Proceeding...
=> Updating GPT/ZFS bootcode on ada1p2
partcode written to ada1p2
bootcode written to ada1
=> Success!
```

**Updating bootcode in a simple GPT-BIOS system:**
```
root@freebsd13vm_2:~ # uname -r
13.1-RELEASE
root@freebsd13vm_2:~ # bootcode-update -g

Boot Partition: [ ada0p1 ]
Disk Serial:    [ VBc3c57d95-9609c4cf ]
Proceed with GPT bootcode update for the following geom: [ada0p1] (Y/n)?: y
Proceeding...
=> Updating GPT bootcode on ada0p1
partcode written to ada0p1
bootcode written to ada0
=> Success!
 ```

**Updating the GPT-BIOS boot with the dryrun flag:**

```
root@mserver: ~# uname -r
12.3-RELEASE-p5
root@mserver: ~# bootcode-update -g -d

Boot Partition: [ ada0p2 ]
Disk Serial:    [ XXX519GYXXXXXX ]
Pool Member:    [ zroot: '/dev/ada0p4' ]
Proceed with GPT/ZFS bootcode update for the following geom: [ada0p2] (Y/n)?: y
Proceeding...
=> Updating GPT/ZFS bootcode on ada0p2 (Dryrun)
gpart bootcode -b /boot/pmbr -p /boot/gptzfsboot -i 2 ada0 (Dryrun)
=> Success! (Dryrun)


Boot Partition: [ ada1p2 ]
Disk Serial:    [ XXX817TM85A3TDXXXXXX ]
Pool Member:    [ zroot: '/dev/ada1p4' ]
Proceed with GPT/ZFS bootcode update for the following geom: [ada1p2] (Y/n)?: y
Proceeding...
=> Updating GPT/ZFS bootcode on ada1p2 (Dryrun)
gpart bootcode -b /boot/pmbr -p /boot/gptzfsboot -i 2 ada1 (Dryrun)
=> Success! (Dryrun)
```

 P.S. Sorry about the clunky code of this beta/experiment utility.
