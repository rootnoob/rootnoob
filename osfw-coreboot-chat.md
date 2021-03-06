<h1>Who is This Post For?</h1>

**Anybody with the following abstract goals**:  
Seeks [ME-neutralised hardware](https://hackaday.com/2016/11/28/neutralizing-intels-management-engine/)  
[Seeks secure, moddable, firmware](https://trmm.net/Thunderstrike/)  
[Seeks a hackable &/ upgradable laptop](https://calbryant.uk/blog/the-ultimate-thinkpad/#) (that preferably only they can hack)  
A laptop that works well with qubes (see [here](https://forum.qubes-os.org/t/community-recommended-computers/5560) for 'just works')  

**Given the above**, this post ought to serve as a quick-hub 'filter' for individuals to find the right balance between new/old, moddable/shiny, etc.  



<details>
  <summary>Question for mods</summary>
[Not sure if this is better suited for general.?] @deeplow  
</details> 

<details>
<summary>Disclaimer</summary>
I will refine this as people criticise and give feedback, for now it's quite high-level: But I hope somebody finds it useful.  
</details>  


<details>  
<summary>Summary</summary>  
This post is intended to be the 'go-to' place on the forum for all questions about Intel-inside laptops for qubes - relating strictly to layers 0,-2, -3 and -4   (explained below).  

<details>
  <summary>Extra Disclaimer</summary>
To prevent this becoming wikipedia, I will reference relevant links; much reading ahoy.  
</details>  

</details>


<details>  
<summary>Firmware/Hardware/Software Layer Abstraction Codes</summary>  

| Layer | Description                          |
|-------|--------------------------------------|
| 0     | Qubes                                |
| -1    | Hypervisor (Xen)                     |
| -2    | Firmware/Bootware                    |
| -3    | Hardware-(me-ware)                   |
| -4    | Physics (design, upgradability, etc) |
</details>  


<details>
<summary>Keeping the list Slim</summary>  
To keep the list slim, at each layer, (excluding layer -1), will be requirements. As this post is criticised and others give feedback, I will update the requirements accordingly.  
</details>  


<details>  
<summary>Layer Requirements</summary>
| Layer | Item                                                                               | M/P | Item                                                                                    | M/P |
|-------|------------------------------------------------------------------------------------|-----|-----------------------------------------------------------------------------------------|-----|
| 0     | [Qubes 4.0.4 & 4.1 Support](https://www.qubes-os.org/doc/system-requirements/)     | M   |                                                                                         |     |
| -2    | [Coreboot](https://www.coreboot.org/)                                              | M   | [Heads Compatible](https://github.com/osresearch/heads)                                 | P   |
| -3    | [<=5th gen intel-core](https://github.com/corna/me_cleaner/wiki/me_cleaner-status) | M   | [TXE not present/removable](https://github.com/corna/me_cleaner/wiki/me_cleaner-status) | P   |
| -4    | Min. 16GB ram & 4 core option                                                      | M   | Min 32gb ram & 6 core option                                                            | P   |
</details>    

<h2>Current List (keep checking)</h2>  

| Brand                                          | Model                                                | rYear | CPU<br>Max                                                                                                                                        | TDP(s)                                                 | Cores | RAM<br>Max | Heads                                                 |
|------------------------------------------------|------------------------------------------------------|-------|---------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------|-------|------------|-------------------------------------------------------|
| [Lenovo](https://en.wikipedia.org/wiki/Lenovo) | [T430](https://www.thinkwiki.org/wiki/Category:T430) | 2012  | [i7-3-QM](https://ark.intel.com/content/www/us/en/ark/products/70846/intel-core-i7-3840qm-processor-8m-cache-up-to-3-80-ghz.html)                 | 35/45W                                                 | 2-4   | 16GB       | yes                                                   |
| [Lenovo](https://en.wikipedia.org/wiki/Lenovo) | [X230](https://www.thinkwiki.org/wiki/Category:X230) | 2012  | [i7-3-QE](https://ark.intel.com/content/www/us/en/ark/products/65709/intel-core-i7-3615qe-processor-6m-cache-up-to-3-30-ghz.html)                 | [13-45W](https://www.xyte.ch/thinkpads/x230/)          | 2-4   | 16GB       | yes                                                   |
| [Lenovo](https://en.wikipedia.org/wiki/Lenovo) | [W530](https://www.thinkwiki.org/wiki/Category:W530) | 2012  | [i7-3-XM](https://ark.intel.com/content/www/us/en/ark/products/71096/intel-core-i7-3940xm-processor-extreme-edition-8m-cache-up-to-3-90-ghz.html) | [35-55W](https://www.thinkwiki.org/wiki/Category:W530) | 2-4   | 32GB       | [TBC](https://github.com/osresearch/heads/issues/616) |
  
<details>  
  <summary>FaQ</summary>  
  
**Why Intel-only?**  
If, (you know of any open-source projects that document how to neutralise AMD-PSP, (and know of any heads equivs, etc)): I will revise this.      
**Why would anybody worry about Intel ME as a threat?**   
We all have different Threat Models - Defense in Depth is always better than none.    
**Why have you only mentioned coreboot & heads?**  
I am not aware of any equivalents that satisfy the other requirements.  
I am not aware of any 'stable' equivs. that satisfy the other requirements.  
**Why 16gb ram min, 32gb preferred?**  
To tame R4.1 && most use-cases 16gb is required min. 32gb is preferred for long-term support.   
**Why TXE removable preferred?**  
Because me_cleaner now supports this, and it is DiD at little added cost.  
**Why 4 core-option minimum?**  
Because some of us like to pin CPU0 to dom0 for security.  
**Why 16gb ram min, 32gb preferred?**  
To tame R4.1 && most use-cases 16gb is required min. 32gb is preferred for long-term support.  
**Why TXE removable preferred?**  
Because me_cleaner now supports this, and it is DiD at little added cost.  
**Why 4 core-option minimum?**  
Because some of us like to pin CPU0 to dom0 for security.  
**Why <= 5th gen intel-core?**    
Because only that years TXE has been confirmed removable.  
Every additional generation is more complex hardware, not just Intel ME but the mobo, firmware etc, and I do not have a holistic understanding of all the extra complexity - so I deem it an unacceptable risk.  

</details>


<details>  
  <summary>Credits (not possible without):</summary>
@Sven for the [HCL](https://www.qubes-os.org/hcl/) & [Community-Recommended List](https://forum.qubes-os.org/t/community-recommended-computers/5560)  
@deeplow for keeping it tidy ;)  
All the core-team, mod and admin team.  
All those who took the time to read, and everyone who is signed-up to the forum ;)  
</details>  
