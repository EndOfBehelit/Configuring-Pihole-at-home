# Setting up Pi-hole at Home
A step-by-step guide on how to set up Pi-hole on a Raspberry Pi.

# Materials needed

  - 1 × Raspberry Pi Zero 2W (other models can also work)
  - 1 x microSD card (I used a 64 GB one, but smaller sizes will also work)
  - 1 x micro-USB charger
  - 3D-printed a case for the Raspberry Pi, NOT ESSENTIAL (I will upload the stl for those interested)

    <img width="917" height="458" alt="imagen" src="https://github.com/user-attachments/assets/b33a6391-cb62-4451-b281-5d774aff3a15" />


# Download Raspberry Pi Imager

Download the Raspberry Pi Imager from the official website: `https://www.raspberrypi.com/software/`. (I used the windows version)

<img width="886" height="275" alt="imagen" src="https://github.com/user-attachments/assets/97a7493d-d5b5-46c6-8732-a263a9ff7c5e" />

<img width="886" height="816" alt="imagen" src="https://github.com/user-attachments/assets/a4b0b828-f596-4d2e-858b-7b0f07d5b6be" />



At this point, insert the microSD in the computer to install the OS and execute the imager.

# Install Raspberry Pi OS

You'll need to choose which model of Raspberry to be used, the OS version and where it's going to be installed.

In this case, I used a Raspberry Pi Zero 2W:

<img width="886" height="614" alt="imagen" src="https://github.com/user-attachments/assets/249390a3-2711-4552-9677-faf6d9f5bedf" />

For the OS you can use the 64bits recommended version, but the Lite version will also be enough:

<img width="886" height="603" alt="imagen" src="https://github.com/user-attachments/assets/7188c772-daad-4cd1-b508-8c8863ffb9ae" />

<img width="886" height="615" alt="imagen" src="https://github.com/user-attachments/assets/86eed88b-8251-4909-a018-2dcea6328358" />

Finally the storage will be the microSD:

<img width="886" height="621" alt="imagen" src="https://github.com/user-attachments/assets/f48057a4-a26f-45f3-9005-0254301ae6e0" />


# Configure Raspberry Pi

Before installing the OS, we need to edit some settings:

Host → This will be the name for the URL (http://example.local/admin)

User and pass → For the Linux user inside the Raspberry

LAN → SSID and password of the Wi-Fi network where the Raspberry Pi will connect (⚠️IMPORTANT!!⚠️ It must be a 2.4Ghz Wi-Fi)

COUNTRY

Timezone

<img width="886" height="673" alt="imagen" src="https://github.com/user-attachments/assets/2a95a620-a978-4823-9331-41dc350d79e2" />

<img width="873" height="728" alt="imagen" src="https://github.com/user-attachments/assets/d480c41f-ec2b-4b08-a512-6267cebdad43" />


*⚠️ If you use a 5 GHz Wi-Fi network, it won’t work!!!⚠️*

In case you have a 5.0 Wi-Fi, you will need to configure in your router a 2.4 Wi-Fi (it's important to have the same host in the IP addresses) and connect there the pihole. The Raspberry is going to block ads from all the Wi-Fi, 2.4 or 5.0 if the host in the IP addresses it's the same. If everything went well, the LED will be on.

Once the OS finishes the installation, you can take the microSD and insert it in the Raspberry. The Raspberry Pi has three connections (HDMI, USB OTG, and Power) and one microSD slot. Ironically, to power the Raspberry Pi, you have to use the USB port with the charger, not the dedicated power port.

<img width="1063" height="603" alt="imagen" src="https://github.com/user-attachments/assets/aa9a186e-a287-4270-8cb1-be2b222e80f3" />

Now you can use SSH to access the Raspberry Pi from your computer: `ssh username@host.local` (The IP can be used too ssh username@X.X.X.X)

<img width="886" height="362" alt="imagen" src="https://github.com/user-attachments/assets/8093580a-eaf5-41ff-9950-bddf59d78687" />


# Configure network with Raspberry Pi as DNS

Now there are 2 important things; we need to know the IP of the Raspberry in our network and we need to make that IP static, to make sure it will always be the same. This depends on which router you have, so it's not going to be guided step by step.

<img width="677" height="565" alt="imagen" src="https://github.com/user-attachments/assets/b030f4ff-67c5-4d62-a85d-b932a764cbda" />

In my case, the IP of my Raspberry is the `192.168.1.166`, so I will make it a reserved one:

<img width="490" height="575" alt="imagen" src="https://github.com/user-attachments/assets/328294ad-97bd-4bc6-94c8-50d7ee6e585d" />

Once inside, run this command to install pi-hole: `curl -sSL https://install.pi-hole.net | bash`

<img width="886" height="702" alt="imagen" src="https://github.com/user-attachments/assets/33d2b88d-4653-413d-a526-b30da47852b3" />

And now, we can start configuring the PiHole:

Here the PiHole warns us about the static IP:

<img width="886" height="639" alt="imagen" src="https://github.com/user-attachments/assets/dd562877-528e-414e-8566-7bc56878a0ed" />

We need to choose which DNS service Pi-hole will use to make a port forwarding (I chose Cloudfare, but you can use the Google DNS or other):

<img width="886" height="571" alt="imagen" src="https://github.com/user-attachments/assets/1a2f9483-68f6-4dfb-a972-b238f925fce2" />

PiHole offers us a default block list, which can be modified or expanded later:

<img width="677" height="450" alt="imagen" src="https://github.com/user-attachments/assets/f0ca4c9e-7cf0-4622-806d-7d9bb72de6f8" />

Query logging creates a record of the queries sent and blocked:

<img width="886" height="575" alt="imagen" src="https://github.com/user-attachments/assets/01132c37-3fc3-4211-8a53-7a01af76ed60" />

Then you need to choose a privacy level, if you don’t want logs, the Anonymous mode works well, but I recommend first using the 0 mode, to see where are you blocking adds, trying to filter and modifying the block list and later change it to anonymous.

To change the privacy level later, you need to modify the property in the `/etc/pihole/pihole.toml`. With the command `grep -n privacylevel pihole.toml` you will see in which line is the property, later run `sudo nano -c +(grep result) pihole.toml`.

<img width="886" height="575" alt="imagen" src="https://github.com/user-attachments/assets/3f413cff-d498-41bc-aca3-a3778300a273" />

This creates a default password, but I'm going to change it.

<img width="886" height="553" alt="imagen" src="https://github.com/user-attachments/assets/6b3b9259-a0f1-4600-989c-16b58fd93883" />

## Change password

In the URL `https://piadd.local/admin` (This URL is only accesible if you are in the same wifi)

<img width="886" height="804" alt="imagen" src="https://github.com/user-attachments/assets/0f163268-fc9b-45b3-9850-25af66bff59e" />

Go back to the ssh console and use the command with sudo `sudo pihole setpassword`:

<img width="886" height="680" alt="imagen" src="https://github.com/user-attachments/assets/5397bfe1-23d1-4a69-b18e-91c001c5bdc7" />

We can enter now the PiHole, but it won't be receiving or blocking querys:

<img width="886" height="560" alt="imagen" src="https://github.com/user-attachments/assets/72d582d6-98ce-4c47-bd7b-c0dbfe759084" />

You'll need to configure our PiHole as the DNS in the router, then the PiHole will make a port forwarding to Cloudfare (or the DNS you chose before) after filtering the querys.

As I mentioned before, this depends on which router you have, so there’s no specific guide.

<img width="886" height="277" alt="imagen" src="https://github.com/user-attachments/assets/648e2ef1-879a-4de7-8572-967579699892" />

# Adding domains to the block list

In the Domains section you can add domains or RegEx to filter the querys, for example, this RegEx filter the Disney+ ads: `diproton-ads-[^\.]*\.hulu\.com\.akadns\.net`

<img width="1243" height="839" alt="imagen" src="https://github.com/user-attachments/assets/0e9147fe-6df6-4478-a949-ab79f4ffcc33" />


When everything is working the Dashboard should show something like this:

<img width="1247" height="944" alt="imagen" src="https://github.com/user-attachments/assets/064923fa-8ca5-41ff-8e20-50f571506e40" />


<img width="902" height="555" alt="imagen" src="https://github.com/user-attachments/assets/f41f60fc-acde-431a-b598-efc795faa6d7" />



