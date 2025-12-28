---
title: "My Favorite Tools"
date: 2025-12-25T14:30:20+01:00
draft: false
---

{{< post-img src="tools2.png" alt="Tools" style="width:200px" >}}

I rewrote this article so it would be true to its name. It used to be a random list of tools I moved to [Hacking Tools]({{< ref "/posts/Hacking-Tools/index.md" >}} "Hacking Tools") and here I will only talk about the very few tools I like and use the most. I chose to embrace modernity
and most of my stack is modern "go/rust and such" based alternatives to legacy tools. I will give one tool per category or utility. You also might find many things from [project discovery](https://docs.projectdiscovery.io/home). I like those guys work very much.

## Reconnaissance and Scanners

One would immediately say "nmap" and be right but many improved nmap already and
I chose to work with [rustscan](https://github.com/bee-san/RustScan) as it is "Fast as F$ck Boi"
it is written in rust and can even work with nmap. Sometimes I might use [naabu](https://docs.projectdiscovery.io/opensource/naabu/overview) too. My classic process is discovering
open ports with rustscan, then look at them closely with nmap. For common vulnerabilities
scanning [nuclei](https://docs.projectdiscovery.io/opensource/nuclei/overview) is a very good option.

## Web content discovery

[ffuf](https://github.com/ffuf/ffuf) is my favorite one and [feroxbuster](https://feroxbuster.com/) seems to be the major contenders here. I am thinking
about ditching gobuster (which is also very fast tho) to simply master ffuf.

## Subdomains enumeration

Here it is usually recommended to try multiple tools to avoid missing some information.
I keep two: [Amass](https://github.com/owasp-amass/amass) and [Subfinder](https://github.com/projectdiscovery/subfinder). Sometimes [katana](https://docs.projectdiscovery.io/opensource/katana/overview) finds stuff I might have missed.

## Web security proxies

[Caido](https://caido.io/fr) and I want to see them grow and actually be worth replacing [Burp](https://portswigger.net/burp). Most of other tools I might need for web would be circonstancial
or crafted for acute exploitation. Also note that things like [metasploit](https://www.metasploit.com/) and the [exploit db](https://www.exploit-db.com/) have almost no serious contenders

## RE and Pwn

Actually the first tool needed here is your brain and second would be python (Pwn and automation mostly) but [pwndbg](https://pwndbg.re/stable/) is very a very good extension of the good ol' gdb.
[Ghidra](https://github.com/NationalSecurityAgency/ghidra) is the most powerful free option for RE and [Binary Ninja](https://binary.ninja/) looks cool...IDA free is not enough while the Pro version will cost you an arm and leg.

## Networks security

[Wireshark](https://www.wireshark.org/) is obviously a must and unbeatten so far


## Miscellanous

Irronically this would be the most important category here because as a hacker the best tool
for you would be the one you built yourself...perfectly tailored for your use cases and fine-tuned
to the kind of things you want to "hack". Therefore automation and exploit crafting is a must (yes,
even if you are on the blue side). Well this is my personal top pick of tools and this will be
updated when I find tools that fit my needs and that I use very often. I am making my own hacking
tools but shhh...I will tell you more soon. You can find a more extensive list of hacking tools
[right here]({{< ref "/posts/Hacking-Tools/index.md" >}}).

