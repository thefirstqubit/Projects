# Project:  Compromised macOS:  Win.Trojan R57-2 & Potentional Root Compromise 

This is a real-life security incident that occured on my Macbook and its OS. What was originally intended to be a home network strengthening lab turned out to be an actual, real security incident. 

Brief Summary:



The first instance of (what I thought was potentially but turned out to be true) a threat detection occured while booting up VMware Fusion to use Kali Linux. While attempting to boot, a notification alert said it could not launch due to the Debian image file having been moved. This was suspicious because I had never moved any files.  Nonetheless, to further investigate I located the Debian image file and proceeded to launch VMware. Upon successfully booting, the virtual machine did not ask for login and password as it always did, bypassing the user login page for Kali Linux altogether. 




I then proceeded to run a clamav While running a clamav scan on my device, I detected two separate paths containing Win.Trojan 57-2 malware. 

<img width="867" alt="5 1_clamscan_trojanfound" src="https://github.com/user-attachments/assets/3db7acf4-c90a-487d-9170-1b5b86930c03" />

Unsure of what to do as a beginner-level cybersecurity analyst, I utilized Google Gemini to assist me in finding a solution to the problem.

 
