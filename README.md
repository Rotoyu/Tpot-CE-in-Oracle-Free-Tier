# Tpot-CE-in-Oracle-Free-Tier
Procedures on how to setup a Tpot Honeypot using Oracle's Free Tier. Setup a Honeypot for free!

## Setting up the account & upgraded to PAYG
Setup account using the followings links:
https://www.oracle.com/cloud/free/
https://docs.cloud.oracle.com/iaas/Content/GSG/Tasks/buysubscription_topic-Upgrade_Your_Free_Promotion.htm

## Preparing the Network

Clicked the Navigation Menu
Clicked Networking
Clicked Reserved Public IP Address
Clicked Reserve public IP Address
Typed tpot_publicIP for the reserved public IP address name (can be anything)
Clicked Reserve Public IP address

Clicked the Navigation Menu
Clicked Networking
Clicked Virtual cloud networks
Clicked VCN
Clicked Actions
Clicked VCN Wizard
Clicked Start VCN Wizard
Typed tpot_vcn for the VCN name (can be anything)
Clicked Next
Clicked Create VCN

## Creating VM

Clicked the Navigation Menu
Clicked Compute
Clicked Instance
Clicked Create Instance
Typed tpot_instance for name (can be anything)
Clicked Change Image
Clicked AlmaLinux
Selected AlmaLinux OS9 (AArch64)
Clicked Select image
Check the Oracle Terms of use Privacy Policy option (may be auto-checked)
Clicked Select image
Clicked Change shape
Selected the arrow next to VM.Standard.A1.Flex (the one that says Always Free-eligible)
Typed 4 for the Number of OCPUs (Max limit)
Clicked Select Shape
Clicked Next, Next
Typed tpot_VNIC for the VNIC name
Select existing virtual cloud network for the Primary network
Selected tpot_vcn for virtual cloud network
Check Automatically assign public IPv4 address
Clicked Download private key
Clicked Next
Clicked Next
Clicked Create
Once the instance is created, note the public IP Address (Replace x.x.x.x with your assigned address.)

## Creating Firewall Rules
Reference: https://github.com/mgrimace/Minecraft-on-Oracle/blob/main/README.md#Forward-ports

Clicked the VM instance
Clicked Networking
Clicked public subnet-tpotVCN
Clicked Default-Security List for tpot_VCN
Clicked Security rules
Clicked Add Ingress Rules
Typed 0.0.0.0/0 
Clicked the Navigation Menu
Clicked Virtual cloud networks
Clicked tpot_VCN
Clicked security
Clicked Create Network Security Group
Typed tpot_NSG
Selected Direction Ingress
Selected Source Type CIDR
Typed 0.0.0.0/0 for Source CIDR
Clicked Create

### Expanded storage

https://github.com/mgrimace/Minecraft-on-Oracle/blob/main/Oracle_additional_settings.md

### Installing tpotce

On terminal, ran sudo chmod 400 /path-to-key/ssh-key-2026-xx-xx.key
Note: I am running this on a linux OS, so I will use chmod to change permissions of the ssh private key. However, if you are on a different OS follow its respective instructions. 

ran the following commands:
ping x.x.x.x (if this fails, your machine is not up or you messed up on the previous steps)
ssh -i "/path-to-key/ssh-key-2026-xx-xx.key" opc@x.x.x.x
sudo dnf update -y && sudo dnf upgrade -y
sudo dnf install curl git firewalld -y
git clone https://github.com/telekom-security/tpotce
./tpotce/install.sh
Pressed y then Pressed Enter
Pressed h then Pressed Enter
Typed Honey for web user name
Pressed y then Pressed Enter
Typed password for web user then Pressed Enter
Typed password again then Pressed Enter
ran sudo reboot

### Accessing tpotce WebUI
Accessed https://x.x.x.x:64297 
Logged in using credentials made when installing tpotce
Look around the services to get hands-on experience with data from a live honeypot

### Accessing VM instance
Typed ssh -i "/path-to-key/ssh-key-2026-xx-xx.key" opc@x.x.x.x -p 64297
