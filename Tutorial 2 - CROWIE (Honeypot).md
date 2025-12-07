What we will learn?

In this tutorial, you will learn how to install and use **Cowrie***. When Cowrie is running on your server, you can capture **attackers** who try to **hack** into your server. You will also learn how to configure Cowrie and create realistic-looking **fake files**, so the attacker wastes time inside the honeypot instead of on your real server.

**This tutorial uses Cowrie on your Tailscale server**, which means your real system stays hidden from public attackers. However, Cowrie itself will still be exposed on your public IP address, because we want to see who is trying to attack us.

When you stop the Cowrie process on your server, your server becomes hidden again (port what using cowrie will automatic hidden in your Tailscale).
You can also place your own payload or files with interesting names to collect attacker information (FOR EDUCATIONAL PURPOSES ONLY).

---

<img width="1038" height="558" alt="1_dNskZQ8sxJGA17rB2ej-hA" src="https://github.com/user-attachments/assets/f62fc603-c97b-4c0b-9634-204eb0f11f47" />

---

## 1. Install python dependencies **(SUDO/ADMIN USER)**

Cowrie is written in Python and requires specific Python dependencies to run. These libraries allow it to simulate an SSH/Telnet environment and properly log everything an attacker does. Without installing the dependencies, Cowrie cannot function or emulate the fake server.

 ```
 sudo apt update
 sudo apt upgrade
sudo apt-get install git python3-virtualenv libssl-dev libffi-dev build-essential libpython3-dev python3-minimal authbind virtualenv
 ```

## 2. Create user account on your server **(SUDO/ADMIN USER)**
Create a new user called "cowrie" without root permissions and without a password using the following commands.
*If you try to run a sudo command as the cowrie user, it will ask you for a password you don’t know — that is normal.*

 ```
sudo adduser --disabled-password cowrie 
su - cowrie
 ```

## 3. Download cowrie **(COWRIE USER)**
In this step you need download "cowrie" on your cowrie user on your server
 ```
git clone http ://github.com/cowrie/cowrie
 ```
## 4. Setup virtual environment **(COWRIE USER)**

Setting up a virtual environment isolates Cowrie's Python packages from the rest of your system. 
Before using Cowrie, you must activate the virtual environment each time. However, if you run Cowrie in the background (which I recommend), you won’t need to activate it again.
 ```
 virtualenv cowrie-env
 source cowrie-env/bin/activate
 pip install --upgrade pip
 pip install --upgrade -r requirements.txt
 ```

## 5. Enable telnet  **(COWRIE USER)**
We need to enable Telnet inside the configuration file.**But first we need "make" file.**
First we need copy file "cowrie.cfg.dist" and paste like "cowrie.cfg"
cp cowrie.cfg.dist cowrie.cfg = making copy of cowrie.cfg.dist and changing her name to cowrie.cfg.

**POSSIBLE ERROR IS PATH TO FILE**

 In my situatoon my location path is like this:
 ```
cp /home/cowrie/cowrie/etc/cowrie.cfg.dist /home/cowrie/cowrie/etc/cowrie.cfg

 ```

Open config file
```
nano /home/cowrie/cowrie/etc/cowrie.cfg
```
You will see this 

<img width="891" height="760" alt="cowrie cfg" src="https://github.com/user-attachments/assets/177623fd-4635-4026-afde-eb9f87cb5a61" />

---

Scroll down and find this and set like this

---

<img width="887" height="747" alt="Cl" src="https://github.com/user-attachments/assets/49afe262-02a0-4635-abb0-a6d03acc9e99" />

---

## 6.Iptables  **(SUDO/ADMIN USER)**
These iptables rules redirect real SSH (port 22) and Telnet (port 23) traffic to Cowrie’s internal ports (2222 for SSH and 2223 for Telnet).
This allows attackers to connect normally to your public SSH/Telnet ports, while actually being routed into the honeypot instead of your real system.

### This commands type at sudo user on your server. 
 ```
sudo iptables -t nat -A PREROUTING -p tcp --dport 22 -j REDIRECT --to-port 2222
sudo iptables -t nat -A PREROUTING -p tcp --dport 23 -j REDIRECT --to-port 2223
 ```
## 7. Start cowrie
Back to folder cd /home/cowrie/cowrie

Run your virtual eivorment 
 ```
source cowrie-env/bin/activate
 ```
You will seen this:

---
<img width="748" height="68" alt="Screenshot 2025-12-07 165844" src="https://github.com/user-attachments/assets/0b37ed2a-cf6c-4244-ae21-780a8ba52b66" />

---
Now run Cowrie using this command for me
 ```
start cowrie
 ```
or (in my case)
```
twistd -n cowrie 
```
---
<img width="955" height="905" alt="Screenshot 2025-12-07 170958" src="https://github.com/user-attachments/assets/35fbeb5e-3623-4cce-bd61-f2b685dd5c50" />

---

We are done — Cowrie is now running on our server. However, if you restart the server, Cowrie will not start automatically and will stay offline.I will show you best way to auto power on.

## 8.Open logs
Cowrie has 2 logs for read that is live logs and older logs (In my case i will use live logs)

 ```
tail -f var/log/cowrie/cowrie.json
 ```
for older logs open  ```/home/cowrie/cowrie/var/log/cowrie ``` and you will see this:

---

<img width="867" height="47" alt="Screenshot 2025-12-07 173921" src="https://github.com/user-attachments/assets/1f04e556-edf9-4fd2-892c-8f8f1df2d05a" />

---

Use commands ``` less -R  ``` + (name of logs) 

















