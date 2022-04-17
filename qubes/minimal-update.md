# Qubes Minimal updateVM


# Linux

<h2>Fedora 35 Minimal</h2>  

1) Copy fedora-35-minimal template, I shall name mine 'f35min-update'.    

2) Run terminal as root on f35min-update (run this command from Dom0 terminal)  
`qvm-run -u=root f35min-update xterm`  

3) Install the following packages inside the template:  
qubes-core-agent-networking  
qubes-core-agent-dom0-updates  
`sudo apt-get install qubes-core-agent-networking qubes-core-agent-dom0-updates`    

Shutdown the VM.  


4) Create an appVM based on the template 'f35min-update', I shall name mine 'updateAppVM'  
Set RAM to 400MB, CPU to 2  
Set provides_network to true  
Set netVM to sys-firewall   


<h3>Disposable updateVM</h3> 

Ensure your Appvm has:
Set disposable_template to true

6.1) Create a new dispVM based on the appVM 'updateAppVM', I shall name mine 'sys-update'  
    Set RAM to 400MB, CPU to 2   
    Set netVM to none  



