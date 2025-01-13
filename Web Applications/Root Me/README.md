This challenge involves both web applications and privilege escalation. It is a guided challenge where we are required to fill in 'checkpoint' like answers to make sure we are on the right track. <br><br>
I first used `nmap` to scan the IP address given.<br><br>
![img](images/1.png)<br><br>
We now know that there are 2 ports open, which answers the first question.<br><br>
I then scanned the IP with the port 80 using `nmap`'s `-sV` option to find out the service version. <br><br>
![img](images/2.png)<br><br>
This gives us the answer to the second question, which is `Apache httpd 2.4.29`.<br><br>
Additionally, port 22 is the default port for the Secure Shell (SSH) protocol. Hence, the answer to the third question is `ssh`.<br><br>
I then used `gobuster` to find the directories on the web server provided.<br><br>
![img](images/3.png)<br><br>
I find two interesting directories, `/panel` and `/uploads`. I first check out the `/panel` directory which gives us the following web page. <br><br>
![img](images/4.png)<br><br>
I then used the PHP reverse shell found on this [github repository](https://github.com/pentestmonkey/php-reverse-shell) to upload a payload. Make sure to change the IP address of the payload to your own and an open port
(in my case, I chose 1234). Then, set up a `netcat` listener on the port of choice and upload the payload. <br><br>
![img](images/5.png)<br><br>
![img](images/6.png)<br><br>
I have now gained access to the shell, and thus was able to find the first flag in `user.txt`.<br><br>
![img](images/7.png)<br><br>
Now, I needed to gain root access. This requires some searching, but one way this could be done is by running the following command: `find / -user root -perm /4000`. This command is essentially looking for a file with SUID (Set User ID) permission, which can then be run with root access. After looking through, I saw that there was something interesting with the `/usr/bin/python`directory.<br><br>
![img](images/8.png)<br><br>
From here, you can go to [GTFOBins](https://gtfobins.github.io/) to look for the Python GTFO bin, which will give us a command that is curated to escalate privileges. Then, I simply placed this command `python -c 'import os; os.execl("/bin/sh", "sh", "-p")'` into the shell that I gained earlier and it gives us root access! <br><br>
![img](images/9.png)<br><br>
From TryHackMe
