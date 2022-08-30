# d11min-usb  

sudo apt install --no-install-recommends qubes-usb-proxy qubes-input-proxy-sender policykit-1 libblockdev-crypto2 ntfs-3g nautilus zenity  

sys-usb: qubes-usb-proxy to provide USB devices to other Qubes and qubes-input-proxy-sender to provide keyboard or mouse input to dom0.  
qubes-usb-proxy is needed wherever you’ll want to use USB  
qubes-input-proxy-sender is needed if you want to use a USB mouse / keyboard  
nautilus & zenity needed to have GUI support in e.g. Qubes backup  
policykit-1 and libblockdev-crypto2 needed to mount encrypted drives  
ntfs-3g needed to be able to mount NTFS formatted drive  
