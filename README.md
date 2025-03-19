
# Suricata IDS/IPS

In this adventure where I started to develop CTI and SOC projects, I realized the installation of Suricata Network IDS/IPS, my second project.

You can find all the LAN and WAN rules I used in my project in this repository.

## System specifications used in the installation.

Ubuntu 24.04 LTS - 4GB RAM - 80GB Storage - 4CPU CORE

## What is Suricata and what does it do?

Suricata is a tool used to ensure network security and take precautions against cyber threats. It monitors and analyzes network traffic, and if it detects any suspicious activity, it alerts us. If properly configured, it can also block attacks. It functions as both an Intrusion Detection System (IDS) and an Intrusion Prevention System (IPS).

Suricata provides benefits such as threat detection, network monitoring, attack prevention, and forensic analysis. Compared to most other products, it stands out with its capabilities and practical use. Let's illustrate this with a visual.

![App Screenshot](https://i.imgur.com/etdCbxE.png)

As seen in the image, we can categorize its capabilities into six main headings. These are anomaly-based detection, signature-based detection, rule engine customization, protocol support, and multi-threading support. In protocol support, it provides support for six protocols: TCP, UDP, HTTP, SMTP, FTP, and DNS.

When we look at its practical use, we can see Network Security Monitoring, Incident Response, and Threat Response, as I mentioned above. While it allows us to monitor network traffic, if properly configured, it can even carry out incident response on its own when it detects threats.

# Suricata’s Features


**Intrusion Detection and Prevention**

Suricata analyzes network traffic to detect malware, attacks, or suspicious activities. If it is properly configured and set to prevention mode, it can automatically stop such threats.


**Network Traffic Monitoring**

It allows us to see what is happening on the network in real-time. For example, we can easily track how much data each device is sending and monitor their activities.


**Protocol Analysis**

Suricata can inspect network protocols such as HTTP, DNS, FTP, SMTP, TCP, and UDP. For instance, if there is suspicious activity in a web request, it can detect it.


**Fast and Efficient**

Thanks to its multi-threading support, it can operate quickly even under heavy traffic loads.


**Flexible Rule System**

Suricata has a customizable rule engine, allowing us to perform analysis based on specific rules. These rules help define suspicious activities. You can use predefined rules or create custom ones.


**Data and File Extraction**

Suricata can capture files passing through the network. It can store them in PCAP format for forensic investigation. This feature is also beneficial for malware analysis.
Advantages of Suricata

    Since it is open-source, it is free to use.
    It has high performance, making it effective even in large networks.
    It is flexible and can function as both an Intrusion Detection System (IDS) and an Intrusion Prevention System (IPS).

## Installation

To install Suricata, we first need to add the repository using PPA (Personal Package Archive). Let's add it now.

```bash
sudo add-apt-repository ppa:oisf/suricata-stable
```

During the installation, the system waits for our confirmation to proceed. We press the Enter key to continue. If we proceed without typing anything, the "Yes" option is selected automatically.

We will use the curl command later. So let's install the curl package now.

```bash
sudo apt-get install curl
```

Yes, we have added the repository and installed curl. Now, let's update our system.

```bash
sudo apt-get update
```

We have updated the repository contents. Now, let's download Suricata.

```bash
sudo apt-get install suricata -y
```

Now, we need to download and extract the Suricata Ruleset. Let's navigate to the **/tmp/ **directory and download it there. After that, we will move the rule files to the **/etc/suricata/rules** directory.

```bash
cd /tmp/ && sudo curl -LO https://rules.emergingthreats.net/open/suricata-6.0.8/emerging.rules.tar.gz
```

Yes, we have downloaded the rules. Now, let's extract them and then move them to the required directory.

```bash
sudo tar -xvzf emerging.rules.tar.gz
sudo mv rules/ /etc/suricata/rules/
```

We have completed the necessary steps, but now we need to adjust the file permissions. Let's configure them right away.

```bash
sudo chmod 640 /etc/suricata/rules/*.rules
```

We have set the necessary permissions. Now it's time to configure the settings. To do this, we need to open the /etc/suricata/suricata.yml file using nano.

There are some important points to pay attention to. You can find them quickly in the terminal using the CTRL + W shortcut.



    HOME_NET → We need to enter the IP address of our Ubuntu machine.
    EXTERNAL_NET → Remove the # symbol at the beginning of the any option and add it before !$HOME_NET.
    default-rule-path → Set /etc/suricata/rules as the rule path.
    rule-files → Change it to *.rules.
    af-packet → Enter the network interface information shown in ifconfig. For most of us, it appears as eth0.

```bash
sudo nano /etc/suricata/suricata.yaml
```

We have completed the necessary configurations. Now, let's restart the Suricata service.

```bash
sudo systemctl restart suricata.service
```
