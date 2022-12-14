# Arkime
### Install Arkime Full Packet Capture tool

` Arkime, also known as Moloch, is an open-source and large-scale indexed packet capture and search tool. It stores and exports all captured packets in PCAP format. You can use Wireshark or other PCAP ingesting tools to analyze the PCAP exported file. Arkime comes with a simple and user-friendly web interface that you can use for browsing, searching, and exporting PCAP. It is designed to be deployed in multiple systems and also able to handle gigabits per second of traffic.`

### Getting Started

#### Before starting, you will need to update your system packages to the latest version.
#### You can update them with the following command:

```
apt-get update -y
```
#### Once all the packages are updated, install the required dependencies using the following command:
```
apt-get install gnupg2 curl wget -y
```
#### Once all the packages are installed, you can proceed to the next step. 

### Installing Arkime 

#### Download the latest version of Arkime from [](arkime.com)
#### we are useing wget command to download the installation file 
```
sudo wget https://s3.amazonaws.com/files.molo.ch/builds/ubuntu-22.04/arkime_4.0.3-1_amd64.deb
```
#### now you can use ls command and locat the downloaded arkime file 
#### the file we hae downloaded is a dpkg pakage so use the following command:
#### is some situations we have to add the X parameter to the file, so use chmod .
```
sudo chmod +x arkime_4.0.3-1_amd64.deb
```
```
sudo dpkg -i arkime_4.0.3-1_amd64.deb
```
#### while the installation we have to be very careful, in the CLI we will get some questions that relate to configering the Arkime in the system 

### Initialize and Elasticsearch Arkime configuration
```      /opt/arkime/db/db.pl http://localhost-ip:9200 init
```
### Add an admin user 
```
      /opt/arkime/bin/arkime_add_user.sh admin "Admin User" THEPASSWORD --admin
```
### Start everything
      systemctl start arkimecapture.service
      systemctl start arkimeviewer.service
      
### Enabling Elasticsearch

#### enable the Elasticsearch service to start at system reboot with the following command:
```
systemctl enable --now elasticsearch
```
#### By default, Elasticsearch listens on port 9200. You can check it with the following command:
```
ss -antpl | grep 9200
```
#### You can also check the Elasticsearch with the following command:
```
curl http://localhost:9200
```
### You should get the following output:
```
{
  "name" : "ubuntu2004",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "9g2B-tNaQl-rjuV32eCgpg",
  "version" : {
    "number" : "7.11.1",
    "build_flavor" : "default",
    "build_type" : "deb",
    "build_hash" : "ff17057114c2199c9c1bbecc727003a907c0db7a",
    "build_date" : "2021-02-15T13:44:09.394032Z",
    "build_snapshot" : false,
    "lucene_version" : "8.7.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```
#### At this point, Elasticsearch is installed and running. You can now proceed to the next step. 

### Look at log files for errors
```
      /opt/arkime/logs/viewer.log
      /opt/arkime/logs/capture.log
```
### Visit http://localhost-ip:8005 with your favorite browser.
      user: admin
      password: THEPASSWORD from step

### For Analysis a PCAP file with the help of Bash code 
##### The code will be uploaded to BIT repo[](github.com/keralahacker/BIT)

#### after using the bash code to upload the PCAP file to arkime local-file we need to restart 
* arkimeviewer.service
* arkimecapture.service
* elasticsearch


## any questions and queries =>=>=> [Vaishnavu C V] 
* [linkedin](linkedin.com/in/vaishnavucv/)
* [iG](https://www.instagram.com/hack_with_vyshu/)
