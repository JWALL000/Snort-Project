## Project Overview 
Welcome to my project! In this project, I successfully configured a working instance of Snort and added a ruleset using PulledPork. In case you're not familiar, Snort is an open-source IDS/IPS system (depending on how it is deployed). In this case, I used it as an Intrusion Detection System (IDS) to parse a known malicious PCAP file and detect suspicious activity.

This project further expanded my knowledge of IDS tools and helped me understand their value in real-world security environments.

Thank you for checking out my project, please see below for the details of how I set it up!

## Step 1

In this step I started by SSH'ing into my ubuntu server, I do this because I find it easier to work from PowerShell on my host as I find it generally more user friendly. 

![Snort-Project1 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%201%20-%20Welcome%20to%20my%20project%20-%20SSHing%20into%20ubuntu%20server.PNG)

## Step 2

Next, It was time to update my Ubuntu server and confirm the upgrade. 

![Snort-Project2 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%202%20-%20Updating%20ubuntu%20server.PNG)

## Step 3

Then, I had to install some prerequisites in order for Snort to work correctly as you can see there was quite a bit to install before we get to installing snort.

![Snort-Project4 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%204%20-%20Installing%20gperftools.PNG)

![Snort-Project5 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%205%20-%20Installing%20ragel.PNG)

This also included locating and installing the newest C ++ libraries. From my understanding, snort is written primarily in C but has some dependencies that rely on C ++ libraries, making this a vital step for snort to function correctly. 

![Snort-Project6 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%206%20-%20Locationg%20boost%20c%2B%2B%20library.PNG)


## Step 4

Next it was time to make a new directory for Hyperscan. Hyperscan is a high speed regex matching engine that is used by snort for rule matching. 

![Snort-Project7 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%207%20-%20Making%20a%20new%20directory%20for%20hyperscan.PNG)

## Step 5

Then, I ensured that the Boost libraries were installed into Hyperscan. 

![Snort-Project8 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%208%20-installing%20c%2B%2B%20libraries%20into%20hyperscan.PNG)

## Step 6

Next, it was time to make a new directory for Hyperbuffers. Hyperbuffers are used in snort as an internal data structure used for efficient packet processing. 

!![Snort-Project9 ](https://github.com/JWALL000/Snort-Project/blob/main/Step-9%20Making%20a%20new%20directory%20for%20flatbuffers.PNG)

## Step 7

After that, it was time to start installing Snort - I went over to the snort website to get instructions for this. 

!![Snort-Project10 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2010%20-%20Getting%20instructions%20from%20the%20snort%20website.PNG)

## Step 8 

Now Snort was installed, It was time to configure it. 

!![Snort-Project11 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2011%20-%20Configuring%20snort%203.PNG)

## Step 9 

After a lot of troubleshooting, snort was now up and running - My main issue is that my usr/bin path was somehow in the wrong order so the binary for Snort couldn't be found, after changing the $PATH, the issue was resolved and snort was running as expected. 

!![Snort-Project12 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2012%20-%20Snort%20finally%20up%20and%20running%20after%20troubleshooting.PNG)

## Step 10 

Next, I had to ensure that two rules were turned off in order for our snort to run correctly - these rules were generic receive-offload and large receive-offload. 

!![Snort-Project13 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2013%20-%20Editing%20file%20to%20turn%20off%20generic%20receive-offload.PNG)


## Step 11 

Now it was time to locate our document file for snort - I got this from a popular cybersecurity youtuber known as Steven (MyDFIR). This was a big help when editing the file correctly. 


!![Snort-Project14 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2014%20-%20Pasting%20and%20configuring%20the%20text%20in%20our%20file%20document.PNG)

After getting the name of our network adapter using ip a, I then input this into the configuration file. 

!![Snort-Project15 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2015%20-%20Adding%20the%20name%20of%20our%20network%20adapter.PNG)

After running the same command - I got confirmation that both rules were off with the correct network adapter. 

!![Snort-Project16 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2016%20-%20Same%20command%2C%20but%20now%20both%20settings%20are%20off.PNG)

## Step 12 

After making a new directory called rules - I edited the nano file to add our new alert rule - this rule had to be 1000001 because snort automatically assigned the first 1000000 rules.
This alert was to pick up ICMP traffic. 

!![Snort-Project17 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2017%20-%20After%20making%20a%20new%20directory%20called%20rules%20-%20I%20edited%20the%20nano%20file%20to%20add%20our%20new%20alert%20rule%20-%20Rule%20had%20to%20be%201000001%20because%20snort%20autmatically%20assigned%20the%20first%201000000%20rules.PNG)

Now we could see our rule was added successfully with no errors. 

!![Snort-Project18 ](https://github.com/JWALL000/Snort-Project/blob/main/STEP18~1.PNG)

## Step 13 

I then configured the rule to get a fast 1 line response to any alerts of ICMP traffic. 

!![Snort-Project19 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2019%20-%20New%20rule%20created%20so%20we%20will%20get%20a%20fast%201%20line%20response%20from%20snort.PNG)

## Step 14 

With snort listening in for ICMP traffic, I decided to test our rule to see if it worked. I did this by pinging the ip of our Ubuntu server. 

!![Snort-Project20 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2020%20-%20Result%20after%20pinging%20in%20a%20new%20powershell%20window%2C%20rule%20works.PNG)

## Step 15 

I next edited the config file so snort knew to use our new rule every time without specifying. 

!![Snort-Project21 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2021%20-%20Setting%20up%20snorts%20configuration%20file%20so%20it%20knows%20where%20to%2)

As you can see, the new rule is a lot shorter.

!![Snort-Project22 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2022%20-%20New%20rule%20-%20alot%20shorter.PNG)

## Step 16 

After another test using ping, we can see our new rule works. 

!![Snort-Project23 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2023%20-%20ICMP%20rule%20working.PNG)


## Step 17 

I then wanted to install PulledPork which is a ruleset for snort 3. This would install multiple rules into our snort for detection of malicious or suspicious activity. 

!![Snort-Project24 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2024%20-%20Installed%20pulled%20pork.PNG)

## Step 18 

Now it was time to edit the config file of PulledPork, using sudo nano - I edited the config file to select the rule set we wanted to use. I decided to use the registired rule set so I set the option from "false" to "true". 
I also had to go over to the Snort site and create an account to generate my oinkcode which is essentially, our API key.

!![Snort-Project25 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2025%20-%20Selecting%20desired%20ruleset%20and%20getting%20oinkcode%20)

## Step 19 

When editing the config, I did run into errors when trying to edit the new rule. The error pointed me over to the pulledpork.py file which is a python file. The error was that the version of PulledPork was unspecified ( left blank ) so after going over to the site I was able to get the version number and fix this error. 

After all that, as you can see - Snort was running with our selected rule set with no errors. 

!![Snort-Project26 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2026%20-%20New%20message%2C%20no%20error.PNG)


## Step 20 

Now it was time to see if the work paid off, I started an instance of snort with our new pulled pork rules and I was relieved to see that it ran with no errors. 


!![Snort-Project27 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2027%20-%20Running%20snort%20with%20pulled%20porks%20rules.PNG)

## Step 21 

I then wanted to see how our new rules would work when analyzing a pcap. So I got a pcap file with known malicious activity inside it from the malware-analysis website. I couldn't recommend this website enough as there is a lot of exercises and PCAPS to use for projects. 

!![Snort-Project28 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2028%20-%20Installing%20packet%20capture%20exercise.PNG)

## Step 22 

I then opened our pcap in snort with our new PulledPork rules and saved that out as a .txt file. I did this so we could cut the file down to what we wanted to see as there was a lot of information to parse through. 

!![Snort-Project29 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2029%20-%20Viewing%20pcap%20in%20snort%20using%20pulled%20porks%20rules%20in%20snort%20%26%20saving%20as%20a%20text%20file.PNG)

Now with the commands below, we can see this information alot clearer. It was clear to see how well snort worked with the installed pulled pork rules. We can even see how many times the detected rules picked up a certain malicious activity as you can see below. 

!![Snort-Project30 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2030%20-%20After%20cutting%20the%20packet%20capture%20to%20get%20more%20readable%20results.PNG)


## Conclusion 

I really enjoyed working on this project, as it familiarized me with how IDS systems work and how useful they can be when configured correctly. I also learned a lot from the troubleshooting process when things weren’t going as planned. This project required a great deal of research and due diligence on my part, as some fixes led me away from the Snort-specific tasks and taught me a lot about how to troubleshoot effectively in a Bash environment.

Thanks for taking the time to view my project - 

Joseph W. 

















