# Project:  Compromised macOS: Win.Trojan R57-2 & Root APT 

This is a real-life security incident that occured on my Macbook and its OS. What was originally intended to be a home network strengthening lab turned out to be an actual, real security incident. 

I learned a bunch of new Linux commands and furthered my skillsets in clamav through this security experience. It was my first time being able to proactively apply NIST 800-61 and I gained extensive insight into IOC analysis.  As a beginner cybersecurity analyst, I found myself in a few positions where I was unsure of how to assess what I was looking at or what steps to take next.  In these moments, I proactively utilized Gemini and effective prompting to aid me in problem solving. 

Tbh, I was a bit stressed and had to stay up all night after checking into a guesthouse for trusted internet connection but I made sure to push through until I was able solve the issue and fully restore my device! It was a great learning experience.

<a href="https://docs.google.com/document/d/1wDaBuVRIQmXg2uPwUFMGU0rKyO-rpt2zUJBy1ySQyKg/edit?usp=sharing">Comprehensive Security Incident Report</a>

# Detection of IOCs and Analyses:

IOC 1: VMware Fusion (moved images) and Kali Linux (user login bypass)

- Unable to boot VMware Fusion after notification alert stating Debian image file had been moved. Highly suspicious because files were never moved. 
- To further investigate, Debian image file were located and proceededed to launch VMware. Upon successful boot, virtual machine bypassed Kali Linux user login page.

*** Double checked with Google Gemini to see if this was suspicious.  Conclusion: YES, run a comprehensive system scan with clamav *** 

IOC 2:  (2) Win.Trojan R57-2 malware infections detected.

<img width="867" alt="5 1_clamscan_trojanfound" src="https://github.com/user-attachments/assets/3db7acf4-c90a-487d-9170-1b5b86930c03" />


IOC 3:  Highly Suspicious Docker Desktop Activity

- Three simultaneous "Docker Desktop" icons appearing in 'apps allowed to run in background' with one instance displaying a missing application icon.

<img width="462" alt="sus_docker_activity" src="https://github.com/user-attachments/assets/d93ecd61-68a9-4cf4-8a19-f2f66d10d1c0" />

- Inability to delete Docker Desktop due to false "running in background" claims. App was clearly shut down.

<img width="1108" alt="docker_running_background" src="https://github.com/user-attachments/assets/c843091a-1bc2-49ca-8786-4f0649d3d794" />

- Persistent reappearance of Docker-related directories after multiple sudo rm -rf attempts, strongly suggesting active root-level persistence mechanisms.

<img width="1056" alt="replication_proof" src="https://github.com/user-attachments/assets/65695727-4399-4635-8e3c-75e3063456a1" />


<img width="1058" alt="unable_delete_2" src="https://github.com/user-attachments/assets/35a6c2b9-8405-4745-8f63-987db9ad9f9b" />

# Response & Recovery

Based on the persistent nature of the threat and root-level compromise, the decision was made to perform a full system wipe as the only reliable containment measure.

- Secure System Wipe: The affected macOS host underwent a complete disk wipe using macOS Recovery and Disk Utility. This ensured the eradication of all operating system files, user data, and embedded malware components from the primary storage.
- Clean OS Reinstallation: macOS was subsequently reinstalled from a trusted source (Apple's recovery servers) onto the now-clean disk.
- Factory reset and re-configuration of home network router and router settings.


# Comments

I learned a bunch of new Linux commands and furthered my skillsets in clamav through this security experience. It was my first time being able to proactively apply NIST 800-61 and I gained extensive insight into IOC analysis.  

As a beginner cybersecurity analyst, I found myself in a few positions where I was unsure of how to assess what I was looking at or what steps to take next.  In these moments, I proactively utilized Gemini and effective prompting to aid me in problem solving. 

Tbh, I was a bit stressed and had to stay up all night after checking into a guesthouse for trusted internet connection but I made sure to push through until I was able solve the issue and fully restore my device! It was a great learning experience.




  

 
