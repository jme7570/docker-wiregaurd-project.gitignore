### docker-wiregaurd-project.gitignore ###

##installing and activating wireguard##

https://m.do.co/c/4d7f4ff9cfe4 this link will make you set up a digital ocean account with a $200 credit towards the account to use

After creating your Digital Ocean account go to your interface and (create) button on top of the website next to your username and select (Droplets). 
It will then take you to an interface where you can create a Virtual Computer (in Digital Ocean

Ubuntu 20.0.4(LTS) x64
Choose a plan: Basic
CPU options: Regular with SSD at $4/mo is basic all you really need if you want more you can do on your own sice you have credit of $200.
Choose a datacenter: New York
Authentication: Password (For this example we use a password, however it is recommended you use SSH keys for a more secure and better establish practice)
Finalize and create: 1 Droplet. Keep host name.
Select Project: first-project

You will then need to install Docker on your Droplet through the SSH window starting with by installing the required tools. Install these tools by typing in: 
** sudo apt install apt-transport-https ca-certificates curl software-properties-common -y **

Docker key next by entering the command:
** curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - **

install a repo based on your systems hardware either in 32 bit or 64 bit
** sudo add-apt-repository \ "deb [arch=amd64] https://download.docker.com/linux/ubuntu \ $(lsb_release -cs) \ stable" **

switch to the correct repository cache into the shell by typing and entering:
** apt-cache policy docker-ce **

install Docker itself by entering the command:
** sudo apt install docker-ce -y **

install its compose file by entering in the shell:
** sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose **
and set its permissions once the compose finishes installing by typing:
** sudo chmod +x /usr/local/bin/docker-compose **

### now you will start the wireguard and downloading the app to your phone ###
Install the Wireguard App on your phone 

mkdir -p ~/wireguard/ 
mkdir -p ~/wireguard/config/ |
compose file in the newly created wireguard folder by typing out the following in shell: 
nano  ** ~/wireguard/docker-compose.yml **


copy and paste the following code block in the file 

-----------------------------------------------------------------------------------

services:
  wireguard:
    container_name: wireguard
    image: linuxserver/wireguard
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Hong_Kong
      - SERVERURL=1.2.3.4
      - SERVERPORT=51820
      - PEERS=pc1,pc2,phone1
      - PEERDNS=auto
      - INTERNAL_SUBNET=10.0.0.0
    ports:
      - 51820:51820/udp
    volumes:
      - type: bind
        source: ./config/
        target: /config/
      - type: bind
        source: /lib/modules
        target: /lib/modules
    restart: always
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
-------------------------------------------------------------------

TZ: Change the Timezone wherever you're at. you can choose what you want at any time 
SERVERURL: Paste the primary IP from your 'Droplet' dashboard interface.
PEERS: Specify the system that you are using to better navigate
then save your work and get out


cd ~/wireguard/ 
and install the Docker compose file by typing in bash: docker-compose up -d  


docker-compose logs -f wireguard 
Scan the QR Code with your phone open an interface to your phones properties and IP, and the endpoint to your server from the Droplet. 
you can go to your phone and click create from QR code to take a picture and then will uplaod itself
once you are here go to IPleak to see your IP address.<img width="1440" alt="Screen Shot 2022-11-30 at 6 27 41 PM" src="https://user-images.githubusercontent.com/112105311/204940044-de7cc90e-f7c3-41cf-94ac-67722627102f.png">
<img width="1440" alt="Screen Shot 2022-11-30 at 6 27 49 PM" src="https://user-images.githubusercontent.com/112105311/204940051-8ffdfbbc-8538-4cbf-a411-6fb1e7a430bb.png">
<img width="1440" alt="Screen Shot 2022-11-30 at 6 28 12 PM" src="https://user-images.githubusercontent.com/112105311/204940054-cd0f1d23-a610-4ef5-94a1-14aafc21c808.png">
<img width="1440" alt="Screen Shot 2022-11-30 at 6 28 53 PM" src="https://user-images.githubusercontent.com/112105311/204940058-ddb4c96d-ae6a-4c25-b7eb-4a086deed415.png">
<img width="1440" alt="Screen Shot 2022-11-30 at 6 42 50 PM" src="https://user-images.githubusercontent.com/112105311/204940060-874ceee5-10d5-48d8-9e65-a82620a23848.png">
<img width="1440" alt="Screen Shot 2022-11-30 at 6 42 57 PM" src="https://user-images.githubusercontent.com/112105311/204940062-0fe7e43d-f189-457d-badb-ff617f4a2ed5.png">





 ![IMG_7021](https://user-images.githubusercontent.com/112105311/204940375-ac471b04-61de-4fb4-b993-7347a67f1473.PNG)
