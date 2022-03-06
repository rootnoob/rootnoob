# Qubes Minimal VPN


# Linux

<h2>Debian 11 Minimal</h2>  

1) Copy debian-11-minimal template, I shall name mine 'deb11-min-vpn'.    

2) Run terminal as root on deb11-min-vpn (run this command from Dom0 terminal)  
`qvm-run deb11-min-vpn xterm -u root`  

3) Install the following packages inside the template:  
qubes-core-agent-networking  
qubes-core-agent-network-manager  
Mandatory Packages:  
`sudo apt-get install qubes-core-agent-networking qubes-core-agent-network-manager`  
For OpenVPN:  
`sudo apt-get install openvpn`  
`sudo apt-get install network-manager-openvpn network-manager-openvpn-gnome`  
For Wireguard:  
`sudo apt-get install wireguard`  

Shutdown the VM.  

<b>Notes:  
Wireguard is integrated into network-manager, but is not in the nm-applet.  
Network-manager gui notifications are not passed through to Dom0 - requires additional package.  </b>


4) Create an appVM based on the template 'deb11-min-vpn', I shall name mine 'vpn-1'  
Set RAM to 400MB, CPU to 2  
Set provides_network to true  
Set netVM to sys-firewall  
Add service 'network-manager'  

5) Adding VPN profiles/configs  
If you would like persistent logs etc, simply add your VPN profiles to networkmanager in the appVM.  
If you would like guarantee that all data is wiped on reboot (no logs, no malware persistence), go to step 6.  

6) Disposable VPN  
All changes in the appvm will be visible to the dispVM. Hence, if you wish to use multiple vpns you may wish to create separate appvms for each respective profile (i.e. one for each location or provider).  

6.1) Create a new appVM based on the template 'deb11-min-vpn', I shall name mine 'vpn-mullvad'  
    Set RAM to 400MB, CPU to 2   
    Set netVM to none  
    Add service 'network-manager'  
    Set disposable_template to true  
  
6.2) From Dom0 terminal, run the following command:  
`qvm-run -u root vpn-mullvad xterm`  

6.3) Copy your VPN config(s) to vpn-mullvad from the VM they are stored, using the qvm-copy command (in the VM which they are stored)  
`qvm-copy vpn-config-file-location`  

6.4) Add VPN config to network-manager via 
From xterm, run the following command:  
`nm-connection-editor`  
Click the + icon, and add your VPN config files.  

Shutdown the VM.  

</b> Notes: Make sure that if adding a password you select 'store this password for all users', else you will need to manually enter the password eacha and every-time you start your dispVM </b>  

6.5) Create a new VM with type: DispVM, based on 'vpn-mullvad', I shall call mine 'mullvad-usa'  
    Set RAM to 400MB, CPU to 2  
    Set netVM to sys-firewall  
    Add service 'network-manager'  
    Set provides_network to true  
    
Simply start your VM using `qvm-start VM` from Dom0 Terminal, and the nm-applet icon will appear in the dom- notification tray. From there you can select the VPN profile to connect to.  
    





