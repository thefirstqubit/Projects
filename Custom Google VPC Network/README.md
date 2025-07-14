# Custom Google Cloud Network w/ Subnets & Firewall Rules #

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


## Create VMs and Test for Latency ##

*test-1 instance* 

gcloud compute instances create us-test-01 \
--subnet subnet-us-west1 \
--zone us-west1-a \
--machine-type e2-standard-2 \
--tags ssh,http,rules

*test-2 instance* 

gcloud compute instances create us-test-03 \
--subnet subnet-europe-west4 \
--zone europe-west4-a \
--machine-type e2-standard-2 \
--tags ssh,http,rules

*test-3 instance* 

gcloud compute instances create us-test-03 \
--subnet subnet-europe-west4 \
--zone europe-west4-a \
--machine-type e2-standard-2 \
--tags ssh,http,rules

<img width="1545" height="408" alt="Screenshot 2025-07-14 at 8 45 16 PM" src="https://github.com/user-attachments/assets/295554bd-749d-4c4d-86fd-88cc36deecc1" />

## Test Latency between VMs with Ping ##

ping -c 3 <us-test-02-external-ip-address>

<img width="560" height="159" alt="Screenshot 2025-07-14 at 8 52 23 PM" src="https://github.com/user-attachments/assets/86d74369-dfbd-44dd-a136-2ee2b74cb4c7" />

## Traceroute and Performance Testing ##

*Install Tracerout*

sudo apt-get update
sudo apt-get -y install traceroute mtr tcpdump iperf whois host dnsutils siege

*use traceroute with websites*

traceroute www.icann.org

traceroute www.wikipedia.org

<img width="802" height="610" alt="Screenshot 2025-07-14 at 9 00 43 PM" src="https://github.com/user-attachments/assets/d1e205e9-0f29-457c-8a82-e8e38b6dc940" />

## iperf to test performance (network throughput and latency ##

*SSH into us-test-02 and install the performance tools*

sudo apt-get update
sudo apt-get -y install traceroute mtr tcpdump iperf whois host dnsutils siege

*SSH into us-test-01 and run*

iperf -s #run in server mode

*On us-test-02 SSH run this iperf*

iperf -c us-test-01.us-west1-a #run in client mode

<img width="1648" height="719" alt="iperf_test 1 3" src="https://github.com/user-attachments/assets/731a8474-079b-4810-bc14-08b4b37ac672" />


