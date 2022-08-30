debian-11-to-minimal  

# WARNING: Broken dependencies. YOU MUST MARK qubes-core packages, else they will be purged.
sudo apt-mark manual qubes-vm-dependencies qubes-core-agent-dom0-updates qubes-core-agent-nautilus qubes-core-agent-passwordless-root qubes-core-agent qubes-core-qrexec qubes-gui-agent qubes-input-proxy-sender qubes-mgmt-salt-vm-connector qubes-usb-proxy qubes-vm-dependencies qubes-db-vm qubesdb xserver-xorg-input-qubes xserver-xorg-qubes-common



sudo apt autoremove  

# Dryrun, check no unintended consequences  
sudo apt remove --purge firefox-esr telnet thunderbird -s  

# Make amendmends  
sudo apt remove --purge firefox-esr telnet thunderbird 


