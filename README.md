# Configuring-Pihole-at-home
Guide about how configure a PiHole at home.

# Materials needed

  - 1 x Raspberry Pi 2W (It can be other models, not necessary this one)
  - 1 x microSD card (I used one with 64GB but it can be less)
  - 1 x micro usb charger
  - I also printed a case for the Raspberry bvut this is not necessary

# Download Raspberry Pi Imager

Download the Raspberry Pi Imager from the official website: `https://www.raspberrypi.com/software/`. (I used the windows version)

<img width="886" height="275" alt="imagen" src="https://github.com/user-attachments/assets/97a7493d-d5b5-46c6-8732-a263a9ff7c5e" />

<img width="886" height="816" alt="imagen" src="https://github.com/user-attachments/assets/a4b0b828-f596-4d2e-858b-7b0f07d5b6be" />


Now insert the microSD in the computer to install the OS and execute the imager.

# Install Raspberry Pi OS

It's needed to choose which model of Raspberry it's going to be used, the OS version and where is going to be installed.

In this case it's going to be used a Raspberry Pi Zero 2W:

<img width="886" height="614" alt="imagen" src="https://github.com/user-attachments/assets/249390a3-2711-4552-9677-faf6d9f5bedf" />

For the OS the 64bits recommended version is ok, but the Lite version will be enough for this:

<img width="886" height="603" alt="imagen" src="https://github.com/user-attachments/assets/7188c772-daad-4cd1-b508-8c8863ffb9ae" />

<img width="886" height="615" alt="imagen" src="https://github.com/user-attachments/assets/86eed88b-8251-4909-a018-2dcea6328358" />

Finally the storage will be the microSD:

<img width="886" height="621" alt="imagen" src="https://github.com/user-attachments/assets/f48057a4-a26f-45f3-9005-0254301ae6e0" />


# Configure Raspberry Pi

Before installing the OS, we need to edit some settings:

Host -> This will be the name for the URL (http://example.local/admin)
User and pass -> For the Linux user inside the Raspberry
LAN -> SSID and pass of the wifi where is going to be placed the Raspberry Pi. (IMPORTANT!! It has to be a 2.4Ghz wifi)
COUNTRY
Timezone

<img width="886" height="673" alt="imagen" src="https://github.com/user-attachments/assets/2a95a620-a978-4823-9331-41dc350d79e2" />

<img width="873" height="728" alt="imagen" src="https://github.com/user-attachments/assets/d480c41f-ec2b-4b08-a512-6267cebdad43" />


IF YOU USE A 5.0 WIFI IT'S NOT GOING TO WORK!!
In case you have a 5.0 Wifi, it's needed to configure in your router a 2.4 wifi (important to have the same host in the IP addresses) and connect there the pihole. The Raspberry is going to block adds from all the wifi, 2.4 or 5.0 if the host in the IP addresses it's the same.


# Configure network with Raspberry Pi as DNS
