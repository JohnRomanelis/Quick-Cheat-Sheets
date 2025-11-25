# SSH

## 1. Key Management

Always generate keys on the machine you connect FROM (Client).

To generate a new key pair: 

```bash
ssh-keygen -t ed25519 -C "device-name"
# -t ed25519: The most modern/secure encryption type.
# -C "comment": A label (email or device name) to identify the key later.
```

View your Public Key (to copy it):
```bash
cat ~/.ssh/id_ed25519.pub
```

Copy Key to Server (Automatic Method): Only works if Password Authentication is still ON.
```bash
ssh-copy-id username@server_ip
```

Add Key to Server (Manual Method): Use this if Passwords are OFF or ssh-copy-id fails.
1. On Client: Copy the content of id_ed25519.pub: `cat ~/.ssh/id_ed25519.pub`
2. On Server: Run `nano ~/.ssh/authorized_keys` and paske the key on a new line.

To check who has access: 
```bash
nano ~/.ssh/authorized_keys
```
## 2. Hardening Security

Edit the configuration file on the Server.
```bash
sudo nano /etc/ssh/sshd_config
```
Critical Settings to Change: Ensure these lines exist and are uncommented (no # at the start):
```plaintext
PermitRootLogin no           # Blocks "root" user login
PasswordAuthentication no    # Disables ALL passwords (keys only)
UsePAM yes                   # Standard system module setting
```
**Apply Changes:** Always run this after editing the config.
```bash
sudo systemctl restart ssh
```

## 3. Monitoring Connections

Check for Successful Logins:
```bash
grep "Accepted" /var/log/auth.log
```

Check Login History (Sessions):
```bash
last -a | head -n 20
```

Check for Attacks/Failed Attempts:
```bash
grep "Failed" /var/log/auth.log
```

Verify Logs are Active - Check the timestamp. It should be close to the current time. 
```bash
ls -l /var/log/auth.log
```

## 4. Connectivity Testing

Check if Port 22 is Open (From outside):

 - Web: Go to CanYouSeeMe.org -> Check Port 22.

## 5. Useful Commands

- Disconnect safely: Type `exit`

   
