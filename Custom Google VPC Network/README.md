# Custom Google Cloud Network w/ Subnets & Firewall Rules ##

*Implementation via both GCC GUI and Cloud Shell CLI*

## Setting Region and Zone ##

  gcloud config set compute/zone "Zone"
  export ZONE=$(gcloud config get compute/zone)

  gcloud config set compute/region "Region"
  export REGION=$(gcloud config get compute/region)

## Creating Custom Network ##

  gcloud compute networks create taw-custom-network --subnet-mode custom

*output:*

<img width="636" height="327" alt="Screenshot 2025-07-14 at 5 56 05 AM" src="https://github.com/user-attachments/assets/5060fe77-0c6a-486e-b5f1-1856fb380b1f" />

## Creating 3 Subnets ##

*Region 1:*  
gcloud compute networks subnets create subnet-us-west-1
   --network taw-custom-network \
   --region us-west-1 \
   --range 10.0.0.0/16
   
<img width="800" height="714" alt="subnet_1" src="https://github.com/user-attachments/assets/9a8f5990-c96d-40ec-8c5d-9351f1ded168" />

*Region 2:*
gcloud compute networks subnets create subnet-us-east4
   --network taw-custom-network \
   --region us-east4 \
   --range 10.1.0.0/16
   
<img width="512" height="606" alt="subnet_2" src="https://github.com/user-attachments/assets/a1922908-401c-4247-9891-1f9280e9b71c" />

*Region 3:*
gcloud compute networks subnets create subnet-europe-west1
   --network taw-custom-network \
   --region europe-west1 \
   --range 10.2.0.0/16

<img width="509" height="594" alt="subnet_3" src="https://github.com/user-attachments/assets/6329824c-e58a-4e2c-9e15-29468c88b7fe" />


## Firewall Rules ##

*HTTP Rules for VMs in Network*

gcloud compute firewall-rules create nw101-allow-http \
--allow tcp:80 --network taw-custom-network --source-ranges 0.0.0.0/0 \
--target-tags http

*ICMP Rule*

gcloud compute firewall-rules create "nw101-allow-icmp" --allow icmp --network "taw-custom-network" --target-tags rules

*Internal Comms Rule*

gcloud compute firewall-rules create "nw101-allow-internal" --allow tcp:0-65535,udp:0-65535,icmp --network "taw-custom-network" --source-ranges "10.0.0.0/16","10.2.0.0/16","10.1.0.0/16"

*SSH Rule*

gcloud compute firewall-rules create "nw101-allow-ssh" --allow tcp:22 --network "taw-custom-network" --target-tags "ssh"

*RDP Rule*

gcloud compute firewall-rules create "nw101-allow-rdp" --allow tcp:3389 --network "taw-custom-network"

<img width="1315" height="605" alt="final_firewalls_set" src="https://github.com/user-attachments/assets/8e6d8a1f-1502-4e75-9592-542ad25a9860" />





   

