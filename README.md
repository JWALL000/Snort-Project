## Project Overview 
Welcome to my project! In this project, I successfully configured a working instance of Snort and added a ruleset using PulledPork. In case you're not familiar, Snort is an open-source IDS/IPS system (depending on how it is deployed). In this case, I used it as an Intrusion Detection System (IDS) to parse a known malicious PCAP file and detect suspicious activity.

This project further expanded my knowledge of IDS tools and helped me understand their value in real-world security environments.

Thank you for checking out my project, please see below for the details of how I set it up!

## Step 1

In this step I started by SSh'ing into my ubuntu server, I do this because I find it easier to work from PowerShell in my host as I find it generally more user friendly. 

![Snort-Project1 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%201%20-%20Welcome%20to%20my%20project%20-%20SSHing%20into%20ubuntu%20server.PNG)

## Step 2

Next, It was time to update my ubuntu server and confirm the upgrade. 

![Snort-Project2 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%202%20-%20Updating%20ubuntu%20server.PNG)

## Step 3

Then, I had to install some prerequisites in order for snort to work correctly as you can see there was quite a bit to install before we get to installing snort.

![Snort-Project4 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%204%20-%20Installing%20gperftools.PNG)

![Snort-Project5 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%205%20-%20Installing%20ragel.PNG)

This also included locating and installing the newest C ++ libraries. From my understanding, snort is written primarily in C but has some dependancies that rely on c ++ libraries, makiung this a vital step for snort to
function correctly. 

![Snort-Project6 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%206%20-%20Locationg%20boost%20c%2B%2B%20library.PNG)


## Step 4

Next it was time to make a new directory for hyperscan. Hyperscan is a high speed regex matching engine that is used by snort for rule matching. 

![Snort-Project7 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%207%20-%20Making%20a%20new%20directory%20for%20hyperscan.PNG)

## Step 5

Then, I ensured that are boost libraries were installed into hyperscan. 

![Snort-Project8 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%208%20-installing%20c%2B%2B%20libraries%20into%20hyperscan.PNG)

## Step 6

Next, it was time to make a new directory for hyperbuffers. Hyperbuffers is used in snort as an internal data structure which is used for efficient packet processing. 

!![Snort-Project9 ](https://github.com/JWALL000/Snort-Project/blob/main/Step-9%20Making%20a%20new%20directory%20for%20flatbuffers.PNG)

## Step 7

After that, it was time to start installing snort - I went over to the snort website to get instructions for this. 

!![Snort-Project10 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2010%20-%20Getting%20instructions%20from%20the%20snort%20website.PNG)

## Step 8 

Now snort was installed, It was time to configure it. 

!![Snort-Project11 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2011%20-%20Configuring%20snort%203.PNG)

## Step 9 

After a lot of troublshooting, snort was now up and runnning - My main issue is that my usr/bin library was somehow in the wrong order so the binary for snort couldnt be found, after changing the $PATH, the issue was resolved and snort was running as expected. 

!![Snort-Project12 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2012%20-%20Snort%20finally%20up%20and%20running%20after%20troubleshooting.PNG)

## Step 10 

Next, I had to ensure that two rules were turned off in order for our snort to run correctly - these rules were gerneric receive-offload and large recieve-offload. 

!![Snort-Project13 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2013%20-%20Editing%20file%20to%20turn%20off%20generic%20receive-offload.PNG)


## Step 11 

Now it was time to locate our document file for snort - I got this from a popular cybersecurity youtuber known as Steven (MyDFIR). This was a big help when editing the file correctly. 


!![Snort-Project14 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2014%20-%20Pasting%20and%20configuring%20the%20text%20in%20our%20file%20document.PNG)

After getting the name of our network adapter using ip a, I then input this into our new setting. 

!![Snort-Project15 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2015%20-%20Adding%20the%20name%20of%20our%20network%20adapter.PNG)

After running the same command - I got confirmation that both rules were off with the correct network adapter. 

!![Snort-Project16 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2016%20-%20Same%20command%2C%20but%20now%20both%20settings%20are%20off.PNG)

## Step 12 

After making a new directory called rules - I edited the nano file to add our new alert rule - this rule had to be 1000001 because snort autmatically assigned the first 1000000 rules.
This alert was to pick up ICMP traffic. 

!![Snort-Project17 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2017%20-%20After%20making%20a%20new%20directory%20called%20rules%20-%20I%20edited%20the%20nano%20file%20to%20add%20our%20new%20alert%20rule%20-%20Rule%20had%20to%20be%201000001%20because%20snort%20autmatically%20assigned%20the%20first%201000000%20rules.PNG)

Now we could see our rule was added successfully with no errors. 

!![Snort-Project18 ](https://github.com/JWALL000/Snort-Project/blob/main/STEP18~1.PNG)

## Step 13 

I then configured the rule to get a fast 1 line response to any alerts of ICMP traffic. 

!![Snort-Project19 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2019%20-%20New%20rule%20created%20so%20we%20will%20get%20a%20fast%201%20line%20response%20from%20snort.PNG)

## Step 14 

With snort listening in for ICMP traffic, I decided to test our rule to see if it worked. I did this my pinging the ip of our ubuntu server. 

!![Snort-Project20 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2020%20-%20Result%20after%20pinging%20in%20a%20new%20powershell%20window%2C%20rule%20works.PNG)

## Step 15 

I next edited the config file so snort knew to use our new rule everytime without specifying. 

!![Snort-Project21 ](https://github.com/JWALL000/Snort-Project/blob/main/Step%2021%20-%20Setting%20up%20snorts%20configuration%20file%20so%20it%20knows%20where%20to%2)

## Step 16 















