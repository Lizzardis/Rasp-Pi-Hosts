# Rasp-Pi-Misc
This is a private collection of tweaks or changes which are used on my Raspberry Pi.

## Update-Script.sh
This Update-Script.sh is an executable .sh script which will automatically update the Raspberry Pi & also update the host lists contained within Pi-Hole.

The script is set to automatically authorise all changes, and then automatically restart the Pi.

## Pi-Hole Query Change
This file contains instructions on how to change the amount of queries that Pi-Hole shows by default in the Query Log. I found that 10 was far too little for the amount of queries my devices made, and needed to see much more. Hence, these instructions increase the default Queries to 100, but also increases the other "Number of Queries" options too.

## Host File
One of the biggest files on this repo is a merged host list which consists of domains from all over which can be used as a central host file for Pi-Hole.

Due to the nature of hosts updates, this list may be wildly out of date for certain block lists which are regularly maintained (StevenBlack, Disconnect, etc).

With this in mind, this is mainly just a copy of certain hosts which aren't regularly updated, but which could disappear due to neglect or deletion.

Below are the host files which have been merged together to make the host file found on this repo.

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