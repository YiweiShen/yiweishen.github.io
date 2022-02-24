---
title: HTTP Proxy via Squid in Ubuntu on Microsoft Azure
date: 2022-02-24 12:34:21
tags:
---

For some reason, you need to use a HTTP Proxy.

Let me assume you have an account of Microsoft Azure. 

# Create VM on Azure
First, go to Azure Portal and create a linux virtual machine, say, Ubuntu 20.04 LTS. Default config will be fine during your VM setup.

# Connect to VM
Connect to the virtual machine via SSH with client, in my case, I use Terminal on MacOS. Let's rename the private key file to azureuser.pem which you download from the previous VM creation step. Use chmod 400 to ensure you have read-only access to the private key. 
```bash
chmod 400 azureuser.pem
ssh -i /Path/To/Some/Folder/azureuser.pem azureuser@vps_IP
```

# Install Squid
```bash
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install squid -y
```

# Update Squid Config file
```bash
sudo nano /etc/squid/squid.conf
```

Find and insert the below two lines BEFORE the line of http_access deny all, to allow your IP to use the proxy.
```bash
acl client src your_IP
http_access allow client
```
By default, Squid uses port 3128. If you are going to change it, just remember to double check if any other application is using the port by default.
```bash
http_port PORT_NUMBER
```
By default, Squid will append your original IP address in the HTTP requests it forwards, something like X-Forwarded-For: 192.1.2.3. So, if you don't want the destination server to know you are using a proxy, and you want to remove some of the request_headers that Squid passes on to the destination server, you can Ctrl + W to find and uncomment these:
```bash
# forwarded_for off
# request_header_access Authorization allow all
# request_header_access Proxy-Authorization allow all
# request_header_access Cache-Control allow all           
# request_header_access Content-Length allow all
# request_header_access Content-Type allow all
# request_header_access Date allow all
# request_header_access Host allow all
# request_header_access If-Modified-Since allow all
# request_header_access Pragma allow all
# request_header_access Accept allow all
# request_header_access Accept-Charset allow all
# request_header_access Accept-Encoding allow all
# request_header_access Accept-Language allow all
# request_header_access Connection allow all
# request_header_access All deny all
```

All, done. Ctrl + O to save the file, and Ctrl + X to exit the file. Restart Squid or maybe you can just restart VM.
```bash
sudo service squid restart
```

# Open Port for Squid
Lastly, go to your VM on the azure portal, open the Networking Tab in the settings. You need to add one inbound port rules to make the Squid http_port number (by default, 3128) accessible from your IP.

# Use HTTP Proxy in Python
```python
import requests

http_proxy = {
	'http': 'http://vps_IP:PORT_NUMBER',
}

r = requests.get(url, proxies=http_proxy)
```

# Use HTTP Proxy on iOS
Go to the settings page of the WiFi you are currently using. Configure HTTP Proxy to Manual and enter the details. 

By the way, save your time and do not use Squid to bypass GFW. It will fail, technically speaking. I'm sorry. 

Squid is not designed to encrypt internet traffic by any means. On the contrary, Squid server can and will intercept SSL interception because Squid is literally the man-in-the-middle (MiTM). Keep that in mind if you consider making use of the other's HTTP Proxy.


Ref:

Ubuntu documentation for Squid:
https://help.ubuntu.com/community/Squid

Squid man page: 
http://manpages.ubuntu.com/manpages/focal/en/man8/squid.8.html

Official Squid site: 
http://www.squid-cache.org
