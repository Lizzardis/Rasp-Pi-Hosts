# Rasp-Pi-Misc
This is a private collection of tweaks or changes which are used on my Raspberry Pi.

## Update-Script.sh
This Update-Script.sh is an executable .sh script which will automatically update the Raspberry Pi & also update the host lists contained within Pi-Hole.

The script is set to automatically authorise all changes, and then automatically restart the Pi.

## Pi-Hole Query Change
This file contains instructions on how to change the amount of queries that Pi-Hole shows by default in the Query Log. I found that 10 was far too little for the amount of queries my devices made, and needed to see much more. Hence, these instructions increase the default Queries to 100, but also increases the other "Number of Queries" options too.

## Master-Hosts File
One of the biggest files on this repo is a merged host list which consists of over 1.3 Million domains from all over which can be used as a central host file for Pi-Hole.

Due to the nature of hosts updates, this list may be wildly out of date for certain block lists which are regularly maintained (StevenBlack, Disconnect, etc). Keeping such a large number of domains in 1 central location might not be good idea... Certain devices don't work well with host files over 10MB & this one is over 25MB. Raspberry Pi's should be fine though. 

I have also consolidated all of the hosts used by the blocklists below, removed any duplicates & meticulously gone through & removed any recurrent sub-domains which all stem from the same domain. This is not only to reduce the number of overall lines, therefore reducing the overall size of the file, but also to block *all* sub-domains for certain domains. This may cause a slight issue for certain use cases, however overall it should not be too much of a problem. Most of the time, if you're blcoking a certain sub-domain, chances are you want the whole domain blocked i.e doubleclick.net

For what it's worth, and to make sure I remember next time, when editing the hosts file, I started by manually looking through for any recurrent top-level domains & making a note of them. Once I'd 
got a few, I'd then CTRL+F in Notepad++, navigate to the "Replace" tab & input the following into the "Find What" box: `.*(nameoftopdomainhere.com)` & then making sure to put "$1" in the "Replace With:" box. This allowed me to quickly, albeit kind of dirtily, remove hundreds of sub-domains at once, leaving behind nothing but multiple lines of the actual domain. 

Ordering the lines A-Z by going to "Edit" > "Line Operations" > "Sort Lines Lexicographically Ascending" & then going back into "Edit" > "Line Operations" then "Remove Duplicate Lines" to take care of the multiple top-level domains left behind, leaving only the 1 domain in the list. This must have been done a *DOZEN* times, to take the overall number of lines down from over 2 Million, to just over 1.3 Million. 

With this in mind though, this host file is mainly just a copy of certain hosts which aren't regularly updated, but which could disappear due to neglect or deletion. I thought it best to have the list of domains for things such as "SmartTVAds", which I doubt is going to be regularly updated.

I'd love to make a script which would collate these host files together, then I could go in & manually edit them, but alas, I might need to do a little bit of research on exactly *how* to do that first. For now, manually doing it is the way forward.

Below are the host files which have been merged together to make the host file found on this repo. If I stumble across any other host lists which I merge into the Master-hosts file, I'll also link it here too.

List Author (A - Z) | List Name | Page Links 
--- | --- | ---  
Abuse.ch | URLhaus Host File | [Raw Page Link](https://urlhaus.abuse.ch/downloads/hostfile/)
AdAway | Default Blocklist | [Raw Page Link](https://adaway.org/hosts.txt)
AmnestyTech | NSO Group Pegasus - Domains | [Github](https://raw.githubusercontent.com/AmnestyTech/investigations/master/2021-07-18_nso/domains.txt)
AmnestyTech | NSO Group Pegasus - Domains - V2 | [Github](https://raw.githubusercontent.com/AmnestyTech/investigations/master/2021-07-18_nso/v2_domains.txt)
AmnestyTech | NSO Group Pegasus - Domains - V3 | [Github](https://raw.githubusercontent.com/AmnestyTech/investigations/master/2021-07-18_nso/v3_domains.txt)
AmnestyTech | NSO Group Pegasus - Domains - V4 | [Github](https://raw.githubusercontent.com/AmnestyTech/investigations/master/2021-07-18_nso/v4_domains.txt)
AmnestyTech | NSO Group Pegasus - Domains - V4 Validation Domains | [Github](https://raw.githubusercontent.com/AmnestyTech/investigations/master/2021-07-18_nso/v4_validation_domains.txt)
Crazy-Max | Windows Spy Blocker | [Github](https://raw.githubusercontent.com/crazy-max/WindowsSpyBlocker/master/data/hosts/spy.txt)
Cyber Threat Coalition | COVID-19 Blocklist | [Raw Page Link](https://blocklist.cyberthreatcoalition.org/vetted/url.txt)
DandelionSprout | AntiMalwareHosts | [Github](https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Alternate%20versions%20Anti-Malware%20List/AntiMalwareHosts.txt)
DeveloperDan | Ads & Tracking Extended | [Raw Page Link](https://www.github.developerdan.com/hosts/lists/ads-and-tracking-extended.txt)
Disconnect.me | Simple Ad List | [Raw Page Link](https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt)
Disconnect.me | Simple Tracking List | [Raw Page Link](https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt)
Disconnect.me | Simple Malvertising List | [Raw Page Link](https://s3.amazonaws.com/lists.disconnect.me/simple_malvertising.txt)
FadeMind | AntiPopAds | [Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/antipopads/hosts)
FadeMind | AnudeepND-blacklist-adservers | [Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/anudeepND-blacklist-adservers/hosts)
FadeMind | Browser Based Crypto Miners | [Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/CoinBlockerList/hosts)
FadeMind | Goodbye-Ads-Youtube-Adblock-Extension | [Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/GoodbyeAds-YouTube-Adblock-Extension/hosts)
FadeMind | Goodbye-Ads-Youtube-Samsung-Extension | [Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/GoodbyeAds-Samsung-Adblock-Extension/hosts)
FadeMind | Goodbye-Ads-Youtube-Xiaomi-Extension | [Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/GoodbyeAds-Xiaomi-Extension/hosts)
FadeMind | Hosts.extra | [Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.2o7Net/hosts)
FadeMind | Lightswitch05-Ads-Tracking-Extended | [Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/Lightswitch05-ads-tracking-extended/hosts)
FadeMind | Spam Hosts | [Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.Spam/hosts)
FadeMind | Risk Hosts | [Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.Risk/hosts)
FadeMind | Unchecky Ads | [Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/UncheckyAds/hosts)
FadeMind | What-Zit-Tooya-Ad-Block | [Github](https://github.com/FadeMind/hosts.extras/raw/master/What-Zit-Tooya-Ad-Block/hosts)
Firebog (WaLLy3K) | AdGuardDNS.txt | [Raw Page Link](https://v.firebog.net/hosts/AdguardDNS.txt)
Firebog (WaLLy3K) | EasyPrivacy.txt | [Raw Page Link](https://v.firebog.net/hosts/Easyprivacy.txt)
Firebog (WaLLy3K) | Prigent-Ads.txt | [Raw Page Link](https://v.firebog.net/hosts/Prigent-Ads.txt)
Firebog (WaLLy3K) | w3kbl.txt | [Raw Page Link](https://v.firebog.net/hosts/static/w3kbl.txt)
Frogeye | First-Party-Trackers List | [Raw Page Link](https://hostfiles.frogeye.fr/firstparty-trackers-hosts.txt)
Frogeye | Multi-Party Trackers | [Raw Page Link](https://hostfiles.frogeye.fr/multiparty-trackers-hosts.txt)
furkun | Protector IP Logger Hosts | [Github](https://raw.githubusercontent.com/furkun/ProtectorHosts/main/hosts)
hkamran80 | SmartTV2 | [Github](https://gist.githubusercontent.com/hkamran80/779019103fcd306979411d44c8d38459/raw/5d5a2950777b9c1ea88d1e7ae5db921b300d9c39/SmartTV2.txt)
llacb47 | Apple-Telemetry | [Github](https://raw.githubusercontent.com/llacb47/mischosts/master/apple-telemetry)
llacb47 | Blacklist | [Github](https://raw.githubusercontent.com/llacb47/mischosts/master/blacklist)
llacb47 | Microsoft-Telemetry | [Github](https://github.com/llacb47/mischosts/raw/master/microsoft-telemetry)
llacb47 | Streaming-Hosts | [Github](https://github.com/llacb47/mischosts/raw/master/streaming-hosts)
llacb47 | TikTok-Hosts | [Github](https://raw.githubusercontent.com/llacb47/mischosts/master/tiktok-hosts)
llacb47 | WhiteOps-Hosts | [Github](https://raw.githubusercontent.com/llacb47/mischosts/master/whiteops-hosts)
LunaWatcher | Android-Tracking.txt | [Github](https://raw.githubusercontent.com/LunarWatcher/Pihole-blocklists/master/global-blocklist-plain.txt)
Matomo-org | Spammers.txt | [Github](https://raw.githubusercontent.com/matomo-org/referrer-spam-blacklist/master/spammers.txt)
NextDNS | Apple Domains | [Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/apple)
NextDNS | Alexa Domains | [Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/alexa)
NextDNS | Huawei Domains | [Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/huawei)
NextDNS | Roku Domains | [Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/roku)
NextDNS | Samsung Domains | [Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/samsung)
NextDNS | Sonos Domains | [Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/sonos)
NextDNS | Windows Domains | [Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/windows)
NextDNS | Xiaomi Domains | [Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/xiaomi)
OISD | Host List | [Raw Page Link](https://dbl.oisd.nl)
Peter Lowe (Yoyo.org) | AdServer List | [Raw Page Link](https://pgl.yoyo.org/adservers/serverlist.php?hostformat=hosts&showintro=0&mimetype=plaintext)
Perflyst | AmazonFireTV.txt | [Github](https://github.com/Perflyst/PiHoleBlocklist/raw/master/AmazonFireTV.txt)
Perflyst | Android-Tracking.txt | [Github](https://github.com/Perflyst/PiHoleBlocklist/raw/master/android-tracking.txt)
Perflyst | SmartTV.txt | [Github](https://github.com/Perflyst/PiHoleBlocklist/raw/master/SmartTV.txt)
QuidsUp | Notrack-Blocklist.txt | [Gitlab](https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-blocklist.txt)
QuidsUp | Notrack-Malware.txt | [Gitlab](https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-malware.txt)
RooneyMcNibNug | SNAFU | [Github](https://raw.githubusercontent.com/RooneyMcNibNug/pihole-stuff/master/SNAFU.txt)
SomeoneWhoCares | Hosts (Zero) | [Raw Page Link](https://someonewhocares.org/hosts/zero/hosts)
Steven Black | Host File | [Github](https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts)
StopForumSpam | Toxic-Domains.txt | [Raw Page Link](https://www.stopforumspam.com/downloads/toxic_domains_whole.txt)
The Block List Project | Tracking.txt | [Raw Page Link](https://blocklistproject.github.io/Lists/tracking.txt)
The Block List Project | Ads.txt | [Raw Page Link](https://blocklistproject.github.io/Lists/ads.txt)
Ubuntu101 | IPs | [Raw Page Link](https://hosts.ubuntu101.co.za/ips.list)
Ubuntu101 | Domains | [Raw Page Link](https://hosts.ubuntu101.co.za/domains.list)
ZeroDot1 | Browser Based Coin Miners | [Gitlab](https://zerodot1.gitlab.io/CoinBlockerLists/hosts_browser)