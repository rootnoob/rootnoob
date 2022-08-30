# d11min-pihole  

#### 

Edit qubes-firewall-user-script  
qvm-run --user=root $PiholeVM "xterm -e 'nano /rw/config/qubes-firewall-user-script'" 
----------[ begin ]-------------  
#!/bin/sh  

This script is called at AppVM boot if this AppVM has the qubes-firewall service enabled. It is executed after the empty chains for the Qubes firewall are created, but before rules for attached qubes are processed and inserted. It is a good place for custom rules and actions that should occur when the firewall service is started. Executable scripts located in /rw/config/qubes-firewall.d are executed immediately before this qubes-firewall-user-script.

# Allow access to Pihole WebGUI from AppVMs  
iptables -I INPUT -s 10.137.0.0/24 -j ACCEPT  
# Allow access to Pihole WebGUI from DispableVMs  
iptables -I INPUT -s 10.138.0.0/16 -j ACCEPT  

# Add a rule that accepts the traffic coming to localhost  
# from XEN's virtual interfaces on port 53  
iptables -I INPUT -i vif+ -p udp --dport 53 -d 127.0.0.1 -j ACCEPT  
----------[ end ]-------------  


# check firewall config  
qvm-run --user root --pass-io --no-gui $PiholeVM 'iptables -L -v'  
qvm-run --user root --pass-io --no-gui $PiholeVM 'iptables -L -v -nat'  

# Anpassung DNSmasg  
qvm-run --user root $PiholeVM "xterm -e 'nano /etc/dnsmasq.conf'"  
# change file to:  
interface=lo  
bind-interfaces  
conf-dir=/etc/dnsmasq.d  

### Setup unbound with NextDNS.io-over-TLS  
See: https://blog.cyclemap.link/2020-01-11-unbound  
# Install & Enable unbound  
qvm-run --pass-io --no-gui --user root $PiholeVM 'apt-get install -y unbound && \  
   systemctl enable unbound'  

# Configure Unbound to use your NextDNS configuration  
qvm-run --user root $PiholeVM 'mkdir -p /etc/unbound/unbound.conf.d'  
qvm-run --user root $PiholeVM "xterm -e 'nano /etc/unbound/unbound.conf.d/pihole.conf'"  
----------[ begin ]-------------  
### Unbound configuration file  
### /etc/unbound/unbound.conf.d/pihole.conf  

### DNS-over-TLS  
server:  
    port: 5300  
    tls-upstream: yes                                            
    tls-cert-bundle: "/etc/ssl/certs/ca-certificates.crt"  

forward-zone:  
  name: "."  
  forward-tls-upstream: yes  
  # insert DNS settings for unbound from NextDNS.io page  
  # Login at NextDNS and then scroll down on the Setup-page  
  forward-addr: 45.90.28.0#<YOURNEXTDNSCONFIGID>.dns1.nextdns.io  
  forward-addr: 2a07:a8c0::#<YOURNEXTDNSCONFIGID>.dns1.nextdns.io  
  forward-addr: 45.90.30.0#<YOURNEXTDNSCONFIGID>.dns2.nextdns.io  
  forward-addr: 2a07:a8c1::#<YOURNEXTDNSCONFIGID>.dns2.nextdns.io  
----------[ end ]-------------  


### Update keys  
qvm-run --pass-io --no-gui --user root $PiholeVM 'update-ca-certificates'  
qvm-run --pass-io --no-gui --user root $PiholeVM 'sudo -u unbound unbound-anchor'  
qvm-run --pass-io --no-gui --user root $PiholeVM 'systemctl restart unbound'  


### reboot  
qvm-shutdown $PiholeVM   
qvm-service $PiholeVM disable-dns-server on  
qvm-prefs $PiholeVM provides_network true  

### finalize installation  
# Set the Pihole-Qube as NetVM  
# Open up a browser in an AppVM and connect to the Pihole IP  
# http://<YOURPIHOLEIP>/admin/settings.php?tab=dns  
# Disable Upstream DNS Servers (on the left)  
# Enable Upstream DNS Servers (on the right)  
#    [X] Custom 1 (IPv4)  
#    127.0.0.1#5300  
# Scroll down and enable DNSSEC  
#    [X] Use DNSSEC  

# Add blocklists via http://<YOURPIHOLEIP>/admin/groups-adists.php  
# You can use my list of blocklists (scroll down)  
# This will add up to ~3.000.000 domains which will be blocked :-)  
# Update blocklists via http://<YOURPIHOLEIP>/admin/gravity.php  

#----[begin blocklists]-----  
# Migrated from /etc/pihole/adlists.list  
https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts  

# No Google - https://github.com/nickspaargaren/no-google/blob/master/README.md  
https://raw.githubusercontent.com/nickspaargaren/no-google/master/pihole-google.txt  

# Suspicious Lists - https://firebog.net	  
https://raw.githubusercontent.com/PolishFiltersTeam/KADhosts/master/KADhosts.txt  
https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.Spam/hosts  
https://v.firebog.net/hosts/static/w3kbl.txt  
https://raw.githubusercontent.com/matomo-org/referrer-spam-blacklist/master/spammers.txt  
https://someonewhocares.org/hosts/zero/hosts  
https://raw.githubusercontent.com/VeleSila/yhosts/master/hosts  
https://winhelp2002.mvps.org/hosts.txt  
https://v.firebog.net/hosts/neohostsbasic.txt  
https://raw.githubusercontent.com/RooneyMcNibNug/pihole-stuff/master/SNAFU.txt  
https://paulgb.github.io/BarbBlock/blacklists/hosts-file.txt  
	
# Advertising List - https://firebog.net/  
https://adaway.org/hosts.txt  
https://v.firebog.net/hosts/AdguardDNS.txt  
https://v.firebog.net/hosts/Admiral.txt  
https://raw.githubusercontent.com/anudeepND/blacklist/master/adservers.txt  
https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt  
https://v.firebog.net/hosts/Easylist.txt  
https://pgl.yoyo.org/adservers/serverlist.php?hostformat=hosts&showintro=0&mimetype=plaintext  
https://raw.githubusercontent.com/FadeMind/hosts.extras/master/UncheckyAds/hosts  
https://raw.githubusercontent.com/bigdargon/hostsVN/master/hosts  
https://raw.githubusercontent.com/jdlingyu/ad-wars/master/hosts  
  
# Tracking & Telemetry List - https://firebog.net  
https://v.firebog.net/hosts/Easyprivacy.txt  
https://v.firebog.net/hosts/Prigent-Ads.txt
https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.2o7Net/hosts
https://raw.githubusercontent.com/crazy-max/WindowsSpyBlocker/master/data/hosts/spy.txt
https://hostfiles.frogeye.fr/firstparty-trackers-hosts.txt
https://hostfiles.frogeye.fr/multiparty-trackers-hosts.txt
https://www.github.developerdan.com/hosts/lists/ads-and-tracking-extended.txt
https://raw.githubusercontent.com/Perflyst/PiHoleBlocklist/master/android-tracking.txt
https://raw.githubusercontent.com/Perflyst/PiHoleBlocklist/master/SmartTV.txt
https://raw.githubusercontent.com/Perflyst/PiHoleBlocklist/master/AmazonFireTV.txt
https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-blocklist.txt  

# Malicious List - https://firebog.net  
https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Alternate%20versions%20Anti-Malware%20List/AntiMalwareHosts.txt
https://osint.digitalside.it/Threat-Intel/lists/latestdomains.txt
https://s3.amazonaws.com/lists.disconnect.me/simple_malvertising.txt
https://v.firebog.net/hosts/Prigent-Crypto.txt
https://bitbucket.org/ethanr/dns-blacklists/raw/8575c9f96e5b4a1308f2f12394abd86d0927a4a0/bad_lists/Mandiant_APT1_Report_Appendix_D.txt
https://phishing.army/download/phishing_army_blocklist_extended.txt
https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-malware.txt
https://raw.githubusercontent.com/Spam404/lists/master/main-blacklist.txt
https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.Risk/hosts
https://urlhaus.abuse.ch/downloads/hostfile/
https://v.firebog.net/hosts/Prigent-Malware.txt
https://v.firebog.net/hosts/Shalla-mal.txt

# Other List - https://firebog.net  
https://zerodot1.gitlab.io/CoinBlockerLists/hosts_browser
https://raw.githubusercontent.com/chadmayfield/my-pihole-blocklists/master/lists/pi_blocklist_porn_all.list
https://raw.githubusercontent.com/chadmayfield/my-pihole-blocklists/master/lists/pi_blocklist_porn_top1m.list
https://raw.githubusercontent.com/anudeepND/blacklist/master/facebook.txt  

# Amazon - https://github.com/bloodhunterd/Pi-hole-Blocklists  
https://github.com/bloodhunterd/Pi-hole-Blocklists/blob/master/Amazon.txt  

# NoTrack - https://gitlab.com/quidsup/notrack-blocklists  
https://gitlab.com/quidsup/notrack-blocklists/-/blob/master/notrack-blocklist.txt
https://gitlab.com/quidsup/notrack-blocklists/-/blob/master/notrack-malware.txt  

# Energized Ultimate - https://github.com/EnergizedProtection/block/blob/master/README.md  
https://block.energized.pro/ultimate/formats/hosts.txt  

# GoodbyeAds -https://github.com/jerryn70/GoodbyeAds/tree/master/Formats  
https://github.com/jerryn70/GoodbyeAds/blob/master/Formats/GoodbyeAds-AdBlock-Filter.txt
https://github.com/jerryn70/GoodbyeAds/blob/master/Formats/GoodbyeAds-Ultra-AdBlock-Filter.txt
https://github.com/jerryn70/GoodbyeAds/blob/master/Formats/GoodbyeAds-YouTube-AdBlock-Filter.txt  

# Energized Regional Extension - https://energized.pro/#download  
https://block.energized.pro/extensions/regional/formats/domains.txt  
