# Qubes Minimal VPN


# Linux

<h2>Debian 11 Minimal</h2>  

1) Copy debian-11-minimal template, we shall name it 'debian-11-minimal-vpn'    
2) Run terminal as root on debian-11-minimal-vpn  
`qvm-run -u root debian-11-minimal-vpn xterm`  
3) Install the following packages:  
qubes-core-agent-networking  
qubes-core-agent-network-manager  
openVPN and/or Wireguard  
`sudo apt-get install qubes-core-agent-networking qubes-core-agent-network-manager`  
`sudo apt-get install openvpn`  
`sudo apt-get install network-manager-openvpn network-manager-openvpn-gnome`

4) Create an appVM based on the template 'debian-11-minimal-vpn', we shall name me it 'vpn-1'  
Set RAM to 400MB, CPU to 2  
Set provides_network to true  
Set netVM to sys-firewall  
Add service 'network-manager'  
