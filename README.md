# Rasp-Pi-Misc
This is a private collection of tweaks or changes which are used on my Raspberry Pi.

## Update-Script.sh
This Update-Script.sh is an executable .sh script which will automatically update the Raspberry Pi & also update the host lists contained within Pi-Hole.

Script needs to reside in /home/pi & be made to be executed by root. Script can be ran using: 
> sudo bash update-script.sh

The script is set to automatically authorise all changes, and then automatically restart the Pi.

## Home-Assistant on Raspberry Pi
After wanting to tinker with Home Assistant on the Raspberry Pi, the documentation seemed to suggest that I needed to reformat the Pi with the Home Assistant image, instead of Raspbain.
This obviously wasn't ideal as I not only wanted to keep my current configuration, but I also wanted to keep my installation of Pi-Hole. Ergo, I searched for another answer & found the following commands from [LazyAdmin.nl](https://lazyadmin.nl/home-network/install-home-assistant-raspberry-pi/) which seemed to install Home Assistant perfectly fine, using Docker.

**Make sure to run the "Update-Script.sh" above to ensure that everything is updated first, before installation of Home Assistant & Docker!**

Now, onto the codes:
 
```
curl -fsSL https://get.docker.com -o get-docker.sh

# Then run:

sudo sh get-docker.sh
```

Once that has finished, you'll want to add the default Pi user into the Docker Group so that the 'Sudo' command does not have to be run every time:

```
sudo usermod -aG docker pi

# Optional Command
sudo chmod 666 /var/run/docker.sock
```

Now that Docker is all sorted, we'll move on to actually installing Home Assistant using the following command:
**NOTE: This command says "raspberrypi3" at the end. If this is being done on a raspberrypi4 (or above) make sure to change that part of the code accordingly**
```
docker run -d \
  --name homeassistant \
  --privileged \
  --restart=unless-stopped \
  -e TZ=MY_TIME_ZONE \
  -v /home/pi/ha:/config \
  --network=host \
  ghcr.io/home-assistant/raspberrypi4-homeassistant:stable
  ```
  
This might take a short while to download & extract. However, once it is done, Home Assistant can be found via the local GUI Webpage found at <raspberrypi_IP>:8123

Head to the webpage & run through the configuration for Home Assistant. 

Next, we have to install Home Assistant Community Store so that we have access to 3rd party integrations *(as we do not have access to them normally since we installed via Docker)*

```
cd /home/pi/ha # This is where the Home Asistant files are stored
# Then run:
wget -O - https://get.hacs.xyz | bash -
```


## Pi-Hole Query Change
This file contains instructions on how to change the amount of queries that Pi-Hole shows by default in the Query Log. I found that 10 was far too little for the amount of queries my devices made, and needed to see much more. Hence, these instructions increase the default Queries to 100, but also increases the other "Number of Queries" options too.

Editing the amount of Queries shown in the recent query logs in Pi Hole can be changed via the following means:

```
sudo nano /var/www/html/admin/scripts/pi-hole/js/queries.js
```

Find this section of code:

```
// If we don't ask filtering and also not for all queries, just request the most recent 100 queries
else if (!("all in GETDict)) {
  APIstring += "=100;
}
```

Then edit the API String to the *largest* amount of queries that should be shown via the dropdown box.

Next, scroll down further & find this code:

```
lengthMenu: [
      [10, 25, 50, 100, -1],
      [10, 25, 50, 100, "All"]
    ],
```

Whichever number is in the left-most slot is the "default" which shows whenever the query log is opened. Changing All to be there is NOT advised. However, all the other numbers can be changed, which will also edit the dropdown too. Like so:

```
lengthmenu: [
 [100, 50, 250, 500, -1],
 [100, 50, 250, 500, "All"]
],
```

However, remember that the APIstring from above needs to also match the *biggest* number you have in this section.

## Pi-Hole Error "Unable to complete update: Contact Support:
This error likely comes from editing the above file to see more of the queries than default. I am assuming that the pihole devs are cross referencing the size of the files on disk, with that of the pihole update to make sure that mostly everything is the same. In this case, it is not.

Rest assured, there is an easy fix, we unfortunately just have to remove the changes with these commands:

Use this command if the "Contact Support" error pops up after the line "/var/www/html/admin"
```
cd /var/www/html/admin
sudo git fetch --tags
sudo git reset --hard
```

Or, use this command if the "Contact Support" error pops up after the line "/etc/.pihole"
```
cd /etc/.pihole
sudo git fetch --tags
sudo git reset --hard
```

Now, the error will probably pop up after the "/var/www/html/admin" line so obviously just use that command to straighten out the error. However, I have included the "/etc/.pihole" one, just in case.

Once the commands have been run though,, you can exit Terminal, open it back up again & run "pihole -up" to update with no issues.

Please keep in mind though... You will have to redo the section above to change the number of visible queries. Shouldn't take *too* long though.

## Master Hosts File
One of the biggest files on this repo is a merged host list which consists of over **3 Million domains** from all over which can be used as a central host file for Pi-Hole.

The single host file comes to over 120MB blocking a whole range of different domains ranging from simple adverts, all the way to phishing servers. 

Ordering the lines A-Z in Notepad++ by going to *"Edit"* > *"Line Operations"* > *"Sort Lines Lexicographically Ascending"* & then going back into *"Edit"* > *"Line Operations"* then *"Remove Duplicate Lines"* to take care of the multiple instances of the same domain. 

Furthermore, some of these lists use the old 127.0.0.1 loopback address. This has also been replaced with 0.0.0.0 - *a non-routable meta-address used to designate an invalid, unknown, or non applicable target* - as it is not only a lot quicker due to there being no wait time for a timeout resolution, but also it seems to be less resource intensive on older machines.

Some lists don't even have the 127.0.0.1 loopback address or 0.0.0.0 meta-address. With this in mind, to keep things uniform, I have added 0.0.0.0 to the beginning of each domain via regular expression in Notepad++. Ctrl + F > Replace > Make sure *"Regular Expression"* is ticked > in the *"Find What:"* box, put: ^ > Then in the *"Replace What:"* box, put 0.0.0.0.

With this in mind though, this host file is mainly just a copy of certain hosts which aren't regularly updated, but which could disappear due to neglect or deletion. I thought it best to have the list of domains for things such as *"SmartTVAds"*, which I doubt is going to be regularly updated.

I'd love to make a script which would collate these host files together, then I could go in & manually edit them, but alas, I might need to do a little bit of research on exactly *how* to do that first. For now, manually doing it is the way forward.

Expand the table below to see the list of host files which have been merged together. If I stumble across any other host lists which I merge into the Master-hosts file, I'll also link it here too.

<details><summary>Click to see table of hosts</summary>
<p>

List Author (A - Z) | List Name | Page Links 
--- | --- | ---  
Abuse.ch | URLhaus Host File | [Raw Page Link](https://urlhaus.abuse.ch/downloads/hostfile/)
AdAway | Default Blocklist | [Raw Page Link](https://adaway.org/hosts.txt)
AmnestyTech | NSO Group Pegasus - Domains | [Raw Github](https://raw.githubusercontent.com/AmnestyTech/investigations/master/2021-07-18_nso/domains.txt)
AmnestyTech | NSO Group Pegasus - Domains - V2 | [Raw Github](https://raw.githubusercontent.com/AmnestyTech/investigations/master/2021-07-18_nso/v2_domains.txt)
AmnestyTech | NSO Group Pegasus - Domains - V3 | [Raw Github](https://raw.githubusercontent.com/AmnestyTech/investigations/master/2021-07-18_nso/v3_domains.txt)
AmnestyTech | NSO Group Pegasus - Domains - V4 | [Raw Github](https://raw.githubusercontent.com/AmnestyTech/investigations/master/2021-07-18_nso/v4_domains.txt)
AmnestyTech | NSO Group Pegasus - Domains - V4 Validation Domains | [Raw Github](https://raw.githubusercontent.com/AmnestyTech/investigations/master/2021-07-18_nso/v4_validation_domains.txt)
Crazy-Max | Windows Spy Blocker | [Raw Github](https://raw.githubusercontent.com/crazy-max/WindowsSpyBlocker/master/data/hosts/spy.txt)
Cyber Threat Coalition | COVID-19 Blocklist | [Raw Page Link](https://blocklist.cyberthreatcoalition.org/vetted/url.txt)
DandelionSprout | AntiMalwareHosts | [Raw Github](https://raw.githubusercontent.com/DandelionSprout/adfilt/master/Alternate%20versions%20Anti-Malware%20List/AntiMalwareHosts.txt)
DeveloperDan | Ads & Tracking Extended | [Raw Page Link](https://www.github.developerdan.com/hosts/lists/ads-and-tracking-extended.txt)
Disconnect.me | Simple Ad List | [Raw Page Link](https://s3.amazonaws.com/lists.disconnect.me/simple_ad.txt)
Disconnect.me | Simple Tracking List | [Raw Page Link](https://s3.amazonaws.com/lists.disconnect.me/simple_tracking.txt)
Disconnect.me | Simple Malvertising List | [Raw Page Link](https://s3.amazonaws.com/lists.disconnect.me/simple_malvertising.txt)
FadeMind | AntiPopAds | [Raw Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/antipopads/hosts)
FadeMind | AnudeepND-blacklist-adservers | [Raw Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/anudeepND-blacklist-adservers/hosts)
FadeMind | Browser Based Crypto Miners | [Raw Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/CoinBlockerList/hosts)
FadeMind | Goodbye-Ads-Youtube-Adblock-Extension | [Raw Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/GoodbyeAds-YouTube-Adblock-Extension/hosts)
FadeMind | Goodbye-Ads-Youtube-Samsung-Extension | [Raw Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/GoodbyeAds-Samsung-Adblock-Extension/hosts)
FadeMind | Goodbye-Ads-Youtube-Xiaomi-Extension | [Raw Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/GoodbyeAds-Xiaomi-Extension/hosts)
FadeMind | Hosts.extra | [Raw Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.2o7Net/hosts)
FadeMind | Lightswitch05-Ads-Tracking-Extended | [Raw Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/Lightswitch05-ads-tracking-extended/hosts)
FadeMind | Spam Hosts | [Raw Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.Spam/hosts)
FadeMind | Risk Hosts | [Raw Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/add.Risk/hosts)
FadeMind | Unchecky Ads | [Raw Github](https://raw.githubusercontent.com/FadeMind/hosts.extras/master/UncheckyAds/hosts)
FadeMind | What-Zit-Tooya-Ad-Block | [Raw Github](https://github.com/FadeMind/hosts.extras/raw/master/What-Zit-Tooya-Ad-Block/hosts)
Firebog (WaLLy3K) | AdGuardDNS.txt | [Raw Page Link](https://v.firebog.net/hosts/AdguardDNS.txt)
Firebog (WaLLy3K) | EasyPrivacy.txt | [Raw Page Link](https://v.firebog.net/hosts/Easyprivacy.txt)
Firebog (WaLLy3K) | Prigent-Ads.txt | [Raw Page Link](https://v.firebog.net/hosts/Prigent-Ads.txt)
Firebog (WaLLy3K) | w3kbl.txt | [Raw Page Link](https://v.firebog.net/hosts/static/w3kbl.txt)
Firestorrrm | iOS Ad List | [Raw Github](https://raw.githubusercontent.com/Firestorrrm/Minimal-Hosts-Blocker/master/iosadlist.txt)
Firestorrrm | Malware List | [Raw Github](https://raw.githubusercontent.com/Firestorrrm/Minimal-Hosts-Blocker/master/malwarelist.txt)
Firestorrrm | moaAB | [Raw Github](https://raw.githubusercontent.com/Firestorrrm/Minimal-Hosts-Blocker/master/moaAB.txt)
Firestorrrm | Youtube Ad List | [Raw Github](https://raw.githubusercontent.com/Firestorrrm/Minimal-Hosts-Blocker/master/youtubeads.txt)
Frogeye | First-Party-Trackers List | [Raw Page Link](https://hostfiles.frogeye.fr/firstparty-trackers-hosts.txt)
Frogeye | Multi-Party Trackers | [Raw Page Link](https://hostfiles.frogeye.fr/multiparty-trackers-hosts.txt)
Fruxlabs | Cyber Threat Intelligence Feeds | [Raw Page Link](https://rescure.fruxlabs.com/rescure_domain_blacklist.txt)
furkun | Protector IP Logger Hosts | [Raw Github](https://raw.githubusercontent.com/furkun/ProtectorHosts/main/hosts)
hkamran80 | SmartTV2 | [Raw Github](https://gist.githubusercontent.com/hkamran80/779019103fcd306979411d44c8d38459/raw/5d5a2950777b9c1ea88d1e7ae5db921b300d9c39/SmartTV2.txt)
KrisIntel | KTIP Malicious Domains | [Raw Page Link](https://kriskintel.com/feeds/ktip_malicious_domains.txt)
llacb47 | Apple-Telemetry | [Raw Github](https://raw.githubusercontent.com/llacb47/mischosts/master/apple-telemetry)
llacb47 | Blacklist | [Raw Github](https://raw.githubusercontent.com/llacb47/mischosts/master/blacklist)
llacb47 | Microsoft-Telemetry | [Raw Github](https://github.com/llacb47/mischosts/raw/master/microsoft-telemetry)
llacb47 | Streaming-Hosts | [Raw Github](https://github.com/llacb47/mischosts/raw/master/streaming-hosts)
llacb47 | TikTok-Hosts | [Raw Github](https://raw.githubusercontent.com/llacb47/mischosts/master/tiktok-hosts)
llacb47 | WhiteOps-Hosts | [Raw Github](https://raw.githubusercontent.com/llacb47/mischosts/master/whiteops-hosts)
LunaWatcher | Global Blocklist | [Raw Github](https://raw.githubusercontent.com/LunarWatcher/Pihole-blocklists/master/global-blocklist-plain.txt)
Matomo-org | Spammers.txt | [Raw Github](https://raw.githubusercontent.com/matomo-org/referrer-spam-blacklist/master/spammers.txt)
NextDNS | Apple Domains | [Raw Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/apple)
NextDNS | Alexa Domains | [Raw Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/alexa)
NextDNS | Huawei Domains | [Raw Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/huawei)
NextDNS | Roku Domains | [Raw Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/roku)
NextDNS | Samsung Domains | [Raw Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/samsung)
NextDNS | Sonos Domains | [Raw Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/sonos)
NextDNS | Windows Domains | [Raw Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/windows)
NextDNS | Xiaomi Domains | [Raw Github](https://raw.githubusercontent.com/nextdns/metadata/master/privacy/native/xiaomi)
OISD | Host List | [Raw Page Link](https://dbl.oisd.nl)
Peter Lowe (Yoyo.org) | AdServer List | [Raw Page Link](https://pgl.yoyo.org/adservers/serverlist.php?hostformat=hosts&showintro=0&mimetype=plaintext)
Perflyst | AmazonFireTV.txt | [Raw Github](https://github.com/Perflyst/PiHoleBlocklist/raw/master/AmazonFireTV.txt)
Perflyst | Android-Tracking.txt | [Raw Github](https://github.com/Perflyst/PiHoleBlocklist/raw/master/android-tracking.txt)
Perflyst | SmartTV.txt | [Raw Github](https://github.com/Perflyst/PiHoleBlocklist/raw/master/SmartTV.txt)
QuidsUp | Notrack-Blocklist.txt | [Gitlab](https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-blocklist.txt)
QuidsUp | Notrack-Malware.txt | [Gitlab](https://gitlab.com/quidsup/notrack-blocklists/raw/master/notrack-malware.txt)
RPiList | MS Office Telemetry | [Raw Github](https://raw.githubusercontent.com/RPiList/specials/master/Blocklisten/MS-Office-Telemetry)
RPiList | Win 10 Telemetry | [Raw Github](https://raw.githubusercontent.com/RPiList/specials/master/Blocklisten/Win10Telemetry)
RooneyMcNibNug | SNAFU | [Raw Github](https://raw.githubusercontent.com/RooneyMcNibNug/pihole-stuff/master/SNAFU.txt)
SomeoneWhoCares | Hosts (Zero) | [Raw Page Link](https://someonewhocares.org/hosts/zero/hosts)
Steven Black | Host File | [Raw Github](https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts)
StopForumSpam | Toxic-Domains.txt | [Raw Page Link](https://www.stopforumspam.com/downloads/toxic_domains_whole.txt)
Technoy | Session-Replay | [Raw Page Link](https://www.technoy.de/lists/Session-Replay.txt)
The Block List Project | Ads.txt | [Raw Github](https://raw.githubusercontent.com/blocklistproject/Lists/master/ads.txt)
The Block List Project | Abuse.txt | [Raw Github](https://raw.githubusercontent.com/blocklistproject/Lists/master/abuse.txt)
The Block List Project | Basic.txt | [Raw Github](https://raw.githubusercontent.com/blocklistproject/Lists/master/basic.txt)
The Block List Project | Fraud.txt | [Raw Github](https://raw.githubusercontent.com/blocklistproject/Lists/master/fraud.txt)
The Block List Project | Malware.txt | [Raw Github](https://raw.githubusercontent.com/blocklistproject/Lists/master/malware.txt)
The Block List Project | Phishing.txt | [Raw Github](https://raw.githubusercontent.com/blocklistproject/Lists/master/phishing.txt)
The Block List Project | Ransomware.txt | [Raw Github](https://raw.githubusercontent.com/blocklistproject/Lists/master/ransomware.txt)
The Block List Project | Redirect.txt | [Raw Github](https://raw.githubusercontent.com/blocklistproject/Lists/master/redirect.txt)
The Block List Project | Scam.txt | [Raw Github](https://raw.githubusercontent.com/blocklistproject/Lists/master/scam.txt)
The Block List Project | Smart-TV.txt | [Raw Github](https://raw.githubusercontent.com/blocklistproject/Lists/master/smart-tv.txt)
The Block List Project | Tracking.txt | [Raw Github](https://raw.githubusercontent.com/blocklistproject/Lists/master/tracking.txt)
The Host File Project | Hosts0.txt | [Raw Page Link](https://hostsfile.mine.nu/hosts0.txt)
Ubuntu101 | Hosts | [Raw Page Link](https://hosts.ubuntu101.co.za/hosts)
Ubuntu101 | IPs | [Raw Page Link](https://hosts.ubuntu101.co.za/ips.list)
Ubuntu101 | Domains | [Raw Page Link](https://hosts.ubuntu101.co.za/domains.list)
Ultimate Hosts Blacklist | hosts0 | [Raw Github](https://raw.githubusercontent.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist/master/hosts/hosts0)
Ultimate Hosts Blacklist | hosts1 | [Raw Github](https://raw.githubusercontent.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist/master/hosts/hosts1)
Ultimate Hosts Blacklist | hosts2 | [Raw Github](https://raw.githubusercontent.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist/master/hosts/hosts2)
Ultimate Hosts Blacklist | hosts3 | [Raw Github](https://raw.githubusercontent.com/Ultimate-Hosts-Blacklist/Ultimate.Hosts.Blacklist/master/hosts/hosts3)
ZeroDot1 | Browser Based Coin Miners | [Gitlab](https://zerodot1.gitlab.io/CoinBlockerLists/hosts_browser)
</p>
</details>