What we will learn?

In this tutorial, you will learn how to install and use Cowrie. When Cowrie is running on your server, you can capture attackers who try to hack into your system. You will also learn how to configure Cowrie and create realistic-looking fake files, so the attacker wastes time inside the honeypot instead of on your real server.

This tutorial uses Cowrie on your Tailscale server, which means your real system stays hidden from public attackers. However, Cowrie itself will still be exposed on your public IP address, because we want to see who is trying to attack us.

When you stop the Cowrie process, your server becomes hidden again.
You can also place your own payload or files with interesting names to collect attacker information (FOR EDUCATIONAL PURPOSES ONLY).

---

<img width="1038" height="558" alt="1_dNskZQ8sxJGA17rB2ej-hA" src="https://github.com/user-attachments/assets/f62fc603-c97b-4c0b-9634-204eb0f11f47" />

---

## 1. Install python dependencies
 ```
 sudo apt update
 sudo apt upgrade
sudo apt-get install git python3-virtualenv libssl-dev libffi-dev build-essential libpython3-dev python3-minimal authbind virtualenv
 ```
## 2. Create user account on your server
Create a new user called "cowrie" without root permissions and without a password using the following commands.
If you try to run a sudo command as the cowrie user, it will ask you for a password you don’t know — that is normal.
 ```
sudo adduser --disabled-password cowrie
su - cowrie
 ```
## 3. Download cowrie
In this step you need download "cowrie" on your cowrie user on your server
 ```
git clone http ://github.com/cowrie/cowri
 ```
## 4. Setup virtual environment
 ```
 virtualenv cowrie-env
 source cowrie-env/bin/activate
 pip install --upgrade pip
 pip install --upgrade -r requirements.txt
 ```
## 5. Enable telnet
 ```
 cp /etc/cowrie.cfg.dist cowrie.cfg
 ```
## 6.Iptables
 ```
sudo iptables -t nat -A PREROUTING -p tcp --dport 22 -j REDIRECT --to-port 2222
sudo iptables -t nat -A PREROUTING -p tcp --dport 23 -j REDIRECT --to-port 2223
 ```
## 7. Start cowrie
 ```
bin/cowrie start
 ```
## 8.live logs
 ```
tail -f ./var/log/cowrie/cowrie.log
 ```

Pokretanje live logova Cowrie kada radi u pozadini (U pozadini I treba raditi)
```
tail -f cowrie/var/log/cowrie/cowrie.json
```
