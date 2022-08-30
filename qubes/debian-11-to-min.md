debian-11-to-minimal  

# WARNING: Broken dependencies. YOU MUST MARK qubes-core packages, else they will be purged.
sudo apt-mark manual qubes-vm-dependencies qubes-core-agent-dom0-updates qubes-core-agent-nautilus qubes-core-agent-passwordless-root qubes-core-agent qubes-core-qrexec qubes-gui-agent qubes-input-proxy-sender qubes-mgmt-salt-vm-connector qubes-usb-proxy qubes-vm-dependencies qubes-db-vm qubesdb xserver-xorg-input-qubes xserver-xorg-qubes-common tinyproxy

# Then:  
sudo apt remove --purge qubes-vm-recompmends  

sudo apt remove --purge python3-qubesimgconverter pulseaudio-qubes qubes-pdf-converter qubes-core-agent-networking qubes-gpg-split pulseaudio pulseaudio-utils libwebrtc-audio-processing-1 firmware-atheros firmware-brcm80211 firmware-intelwimax firmware-ipw2x00 firmware-iwlwifi firmware-linux-nonfree firmware-realtek firmware-zd1211 firmware-ath9k-htc atmel-firmware firmware-amd-graphics firmware-misc-nonfree firmware-linux-free 

sudo apt autoremove  

# Dryrun, check no unintended consequences  
sudo apt remove --purge firefox-esr telnet thunderbird -s  

# Make amendmends  
sudo apt remove --purge firefox-esr telnet thunderbird 


