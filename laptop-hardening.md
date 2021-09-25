| Layer | Description                          |
|-------|--------------------------------------|
| 0     | Qubes                                |
| -1    | Hypervisor (Xen)                     |
| -2    | Firmware/Bootware                    |
| -3    | Hardware-(me-ware)                   |
| -4    | Physics (design, upgradability, etc) |

-4:  
Component removal & customisation. Electronics customsation. MAD failsecure system.  

-3:  
Intel ME Nuked/neutralised.  (upto 3rd gen only to prevent import of extra crapware).  

-2:  
Coreboot-minimal with a customised Heads-minimal image.  
Multifactor boot auth. 
Redundant encrypted disk, multifactor, requires two physical partitions.  

-1:  
Enable FLASK (xen security modules) permanently.  
Isolate CPU0 for dom0  (and for its memory introspection)  
dom0 memory introspection (pinned also to CPU0)  
absolute bare-minimum dom0, (alpine linux for now probably)  

0:  
unikernel firewall, disposable  
Redundant firewall, disposables  
disposable sys-net, sys-usb.  
sys-audio VM.  
sys-gui (where possible)  
split-GPG, split-pass.  
Max utilisation of disposable-vms. Disposable templates to store config files for different base-template variations.  
Strip-down all linux templates to minimal.  
Where using linux: use customised minimal kernels (because nobody needs an entire linux 'kernel'/all the drivers).  
Where being redundant - ensure redundancy is DiD - so if having redundant firewalls, don't use the same kernel.  
Kernel hardening - enforce MAC and research into work for SELinux.  


Usability:  
replace stock icons (which are confusing because they are not qubes-specific icons, they are category icons) with specific icons for each disposable/template etc.  
FInd alt for xfce (pain to customise)  


