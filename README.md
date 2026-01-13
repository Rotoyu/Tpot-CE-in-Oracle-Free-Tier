# Tpot-CE-in-Oracle-Free-Tier
Procedures on how to setup a Tpot Honeypot using Oracle's Free Tier. Setup a Honeypot for free!

## Setting up the account & upgraded to PAYG
Setup account using the followings links:
https://www.oracle.com/cloud/free/
https://docs.cloud.oracle.com/iaas/Content/GSG/Tasks/buysubscription_topic-Upgrade_Your_Free_Promotion.htm

---
## Preparing the Network

1. Clicked the Navigation Menu
2. Clicked Networking
3. Clicked Reserved Public IP Address
4. Clicked Reserve public IP Address
5. Typed tpot_publicIP for the reserved public IP address name (can be anything)
7. Clicked Reserve Public IP address
8. Clicked the Navigation Menu
9. Clicked Networking
10. Clicked Virtual cloud networks
11. Clicked VCN
12. Clicked Actions
13. Clicked VCN Wizard
14. Clicked Start VCN Wizard
15. Typed tpot_vcn for the VCN name (can be anything)
16. Clicked Next
17. Clicked Create VCN

---
## Creating the VM

1. Clicked the Navigation Menu
2. Clicked Compute
3. Clicked Instance
4. Clicked Create Instance
5. Typed tpot_instance for name (can be anything)
6. Clicked Change Image
7. Clicked AlmaLinux
8. Selected AlmaLinux OS9 (AArch64)
9. Clicked Select image
10. Check the Oracle Terms of use Privacy Policy option (may be auto-checked)
11. Clicked Select image
12. Clicked Change shape
13. Selected the arrow next to VM.Standard.A1.Flex (the one that says Always Free-eligible)
14. Typed 4 for the Number of OCPUs (4 is the Max limit for free tier, )
15. Clicked Select Shape
16. Clicked Next, Next
17. Typed tpot_VNIC for the VNIC name
18. Selected existing virtual cloud network for the Primary network
20. Selected tpot_vcn for virtual cloud network
21. Check Automatically assign public IPv4 address
22. Clicked Download private key
23. Clicked Next
24. Clicked Attach block Volume
25. Selected Create new volume for Volume type
26. Typed tpot_block_volume for name
27. Selected Custom for Volume size and performance
28. Typed 200 for Volume size (200 is the limit for the free tier, but choose however much you want. Oracle sets the default as 50)
30. Clicked Attach
31. Clicked Next
32. Clicked Create
33. Once the instance is created, note the public IP Address (Replace x.x.x.x with your assigned address.)

---
## Creating Firewall Rules
Reference: https://github.com/mgrimace/Minecraft-on-Oracle/blob/main/README.md#Forward-ports

1. Clicked the VM instance
2. Clicked Networking
3. Clicked public subnet-tpotVCN
4. Clicked Default-Security List for tpot_VCN
5. Clicked Security rules
6. Clicked Add Ingress Rules
7. Typed 0.0.0.0/0
8. Clicked Add Ingress Rules
7. Typed ::/0 
9. Clicked the Navigation Menu
10. Clicked Virtual cloud networks
11. Clicked tpot_VCN
12. Clicked security
13. Clicked Create Network Security Group
14. Typed tpot_NSG
15. Selected Direction Ingress
16. Selected Source Type CIDR
17. Typed 0.0.0.0/0 for Source CIDR
18. Clicked Create

---
### Installing tpotce

On terminal, ran sudo chmod 400 /path-to-key/ssh-key-2026-xx-xx.key
Note: I am running this on a linux OS, so I will use chmod to change permissions of the ssh private key. However, if you are on a different OS follow its respective instructions. 

ran the following commands:

1. ```ping x.x.x.x (if this fails, your machine is not up or you messed up on the previous steps)```
2. ```ssh -i "/path-to-key/ssh-key-2026-xx-xx.key" opc@x.x.x.x```
3. ```sudo dnf update -y && sudo dnf upgrade -y```
4. ```sudo dnf install curl git firewalld -y```
5. ```git clone https://github.com/telekom-security/tpotce```
6. ```./tpotce/install.sh```
7. Pressed y then Pressed Enter
8. Pressed h then Pressed Enter (I chose hive mode, but if you have less than 4 OCPUs you may need to choose mini with option i)
9. Typed Honey for web user name
10. Pressed y then Pressed Enter
11. Typed password for web user then Pressed Enter
12. Typed password again then pressed Enter
13. ```sudo reboot```

---
### Accessing tpotce WebUI

1. Accessed https://x.x.x.x:64297
2.  Logged in using credentials made when installing tpotce
3.  Look around the services to get hands-on experience with data from a live honeypot

---
### Accessing VM instance
Ran ```ssh -i "/path-to-key/ssh-key-2026-xx-xx.key" opc@x.x.x.x -p 64295```

---
Written by Rotoyu
LICENSE: MIT License. See the License file for details.
