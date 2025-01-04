![img](images/1.png)<br><br>
This is an OSINT (Open Source Intelligence) CTF challenge.<br><br>
The challenge starts off with giving a downloadable file, which is the famous Windows XP background image.<br><br>
![img](images/2.png)<br><br>
The first thing I did was to download the file and use the `exiftool` command to output the metadata of the image.<br><br>
![img](images/3.png)<br><br>
As shown, I can see a variety of information and the first thing that I noticed, was the copyright section, which sats `Copyright: OWoodflint`.<br><br>
I did a google search on the name and a couple websites (Twitter, Github, WordPress) popped up that I assumed related to the challenge. I first took a look at the twitter page.<br><br>
![img](images/4.png)<br><br>
This gave the answer to the first question. `What is this user's avatar of? : cat`.<br><br>
I then looked at the user's first post and saw the BSSID being provided. I used the website [WiGLE: Wireless Network Mapping](https://wigle.net) to find out the SSID of the WAP he connected to, as well as his geolocation.<br><br>
![img](images/6.png)<br><br>
This gave me what I needed for two questions.<br><br>
`What is the SSID of the WAP he connected to? : UnileverWiFi`<br><br>
`What city is this person in? : London`<br><br>
I then turned my attention to his github page.<br><br>
![img](images/5.png)<br><br>
This gave me another answer, his email address.<br><br>
`What is his personal email address? : OWoodflint@gmail.com`<br><br>
Additionally, the github page also confirmed that he was in/from London.<br><br>
The last page that showed up in the Google search was his WordPress blog site.<br><br>
![img](images/7.png)<br><br>
The homepage gave me another answer, which was where he had gone on holiday.<br><br>
`Where has he gone on holiday? : New York`<br><br>
The final question was a bit trickier, but turns out it was hiding in plain sight.<br><br>
I first thought of using `hydra` to brute for his login, but I could not quite find the login page that was within the scope of this challenge. So I decided to look at the page source to see anything interesting.<br><br>
At first, it looked like any other page source, but there was one interesting line that caught my attention.<br><br>
![img](images/8.png)<br><br>
Right underneath the statement on the homepage, there seems have been another text that says `pennYDr0pper.!`, but I was not able to see this on the homepage itself. That was until I realized it was in white.<br><br>
![img](images/9.png)<br><br>
This was the answer to the final question.<br><br>
`What is the person's password? pennYDr0pper.!`<br><br>
From TryHackMe
