# Qubes Minimal Audio


# Linux

<h2>Debian 11 Minimal</h2>  

1) Copy debian-11-minimal template, we shall name it 'deb11-min-web'    
2) Run terminal as root on deb11-min-web  
`qvm-run -u root d11m-audio xterm`  
3) Install the following packages:  
qubes-usb-proxy #necessary for bluetooth  
pulseaudio  
pulseaudio-qubes  
qubes-gui-daemon-pulseaudio  
blueman  
bluez  
pavucontrol  
  

4) Create an appVM based on the template 'deb11-min-web', we shall name me it 'disp11-web'  
Set RAM to 2000MB, CPU to 2  
Set netVM to sys-firewall  


Notes:  Notifications do not appear connecting/connected - requires additional package.  
