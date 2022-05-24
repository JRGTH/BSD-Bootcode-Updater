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

 P.S. Sorry about the clunky code of this beta/experiment utility.
