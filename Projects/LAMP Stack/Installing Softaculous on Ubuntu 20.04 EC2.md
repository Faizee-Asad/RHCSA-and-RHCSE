# 🔧 Project: Installing Softaculous on Ubuntu 20.04 EC2

##📦 Tech Stack

| Component          | Technology                                  |
| ------------------ | ------------------------------------------- |
| OS                 | Ubuntu 20.04 LTS                            |
| Control Panel      | Webuzo (by Softaculous) *(free or premium)* |
| Web Server         | Apache / NGINX                              |
| Software Installer | Softaculous                                 |
| Hosting            | AWS EC2                                     |

# 📝 Step-by-Step Guide to Install Softaculous (via Webuzo)

Softaculous requires a control panel to manage its features. On a raw Ubuntu EC2, the easiest is to use Webuzo, which is made by the same team.

## ✅ Step 1: Launch an Ubuntu 20.04 EC2 Instance

Select Ubuntu Server 22.04 LTS (HVM), 64-bit
Allow ports: 22 (SSH), 80 (HTTP), and 443 (HTTPS)
Choose t2.micro (for testing), with at least 20GB disk

## ✅ Step 2: Connect via SSH
```
ssh -i SSH-KEY.pem ubuntu@<your-ec2-ip>
```

## ✅ Step 3: Download and Install Webuzo
```
wget -N http://files.webuzo.com/install.sh
chmod 0755 install.sh
sudo ./install.sh
```
🕐 This may take 15–30 minutes.

## ✅ Step 4: Access Webuzo Panel
```
http://<your-ec2-ip>:2004
```
You’ll be prompted to set up:
Admin username/password
Domain (you can use EC2 IP)
App stack (LAMP recommended)

## ✅ Step 5: Install Apps with Softaculous

Inside the Webuzo panel:
Go to Enduser Panel
Navigate to Softaculous
Browse or search for apps (e.g., WordPress, Laravel)
Click Install and set options (domain, DB name, admin login)


## ports

| Port     | Panel/Service                           | Protocol  |
| -------- | --------------------------------------- | --------- |
| 2002     | Admin Panel                             | HTTP      |
| 2003     | Enduser Panel                           | HTTP      |
| **2004** | **Enduser Panel (Secure)**              | **HTTPS** |
| 2005     | Webuzo Services (Optional internal use) | -         |
| 2006     | Admin Panel (Secure)                    | HTTPS     |


-------------------------------------------------------------------------------------------
SS

![aws ec2](https://github.com/user-attachments/assets/b6794227-6312-41e8-9041-c60d5aad7400)
![server user](https://github.com/user-attachments/assets/47516bca-78e4-48e6-b6e3-8bff8c25f7fd)
![enduse](https://github.com/user-attachments/assets/eddbac88-4403-4d84-9a4d-c9e1feffee68)
![webuzo_Softaculous](https://github.com/user-attachments/assets/a151e792-5234-4dd5-847a-fff0b1dadea3)
![dns](https://github.com/user-attachments/assets/1c88bc24-28f9-426c-a32b-37b6c91eea8b)
![list ip](https://github.com/user-attachments/assets/55672a9b-9b2f-4a72-afab-f3de198d6c60)
![user created](https://github.com/user-attachments/assets/8c8782ed-4248-4ddf-ae00-cd1038463a88)
![webuzo](https://github.com/user-attachments/assets/8e6def41-1623-428a-b400-5a63c2b87a02)




