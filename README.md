# HoneyPot Setup and Monitoring

A honeypot is a cybersecurity mechanism designed to detect, deflect, or study cyber threats by mimicking a real system to lure attackers. It acts as a decoy, allowing security researchers to monitor unauthorized access attempts, collect data on attack techniques, and analyze malicious activities without risking actual infrastructure. Honeypots can be classified into low-interaction and high-interaction. By deploying honeypots, organizations gain valuable insights into emerging threats, strengthen their defenses, and improve incident response strategies.

# Cowrie Honeypot Setup

Cowrie is a medium to high-interaction SSH and Telnet honeypot designed to log brute-force attacks and shell interaction by attackers.

## 🚀 Features
- Logs brute-force attacks on SSH and Telnet
- Captures attacker commands and interactions
- Emulates a fake filesystem for deception
- Supports file uploads and downloads

## 🛠 Installation

### 1️⃣ Clone the Repository
```sh
git clone https://github.com/nidhipai78/CowrieHoneypot.git
cd CowrieHoneypot
```

### 2️⃣ Setup Virtual Environment (Recommended)
```sh
python3 -m venv cowrie-venv
source cowrie-venv/bin/activate
```

### 3️⃣ Install Dependencies
```sh
pip install -r requirements.txt
```

### 4️⃣ Configure Cowrie
```sh
cp cowrie_example.cfg cowrie.cfg
nano cowrie.cfg
```
Modify parameters such as:
- `listen_port`
- `hostname`
- `log_path`

### 5️⃣ Start the Honeypot
```sh
./start.sh
```
Cowrie logs interactions in `var/log/cowrie/`.

## 🔒 Security Considerations
- **DO NOT** expose Cowrie on a real SSH port (22).
- Ensure the config (`cowrie.cfg`) does not contain private SSH keys or credentials before uploading.
- Use a non-root user to run Cowrie for security.

## 🔄 Running and Managing Cowrie

### Open Python Virtual Environment
```sh
source ~/cowrie/cowrie-venv/bin/activate
```

### Edit Configuration
```sh
nano ~/cowrie/etc/cowrie.cfg
```

### Restart Cowrie
```sh
cd ~/cowrie
./bin/cowrie stop
./bin/cowrie start
```

### Verify if Cowrie is Running
```sh
./bin/cowrie status
```

### View Logs in Real-Time
```sh
tail -f ~/cowrie/var/log/cowrie/cowrie.log
```
To exit, press **Ctrl+C**.

## 📊 Testing the Honeypot

### Simulating an Attacker Session
```sh
ssh root@localhost -p 2222
```

#### Inside the Fake Session - Execute the Following Commands
- **Check System Info:**
  ```sh
  uname -a
  ```
- **List Files:**
  ```sh
  ls -l
  ```
- **Check Active Processes:**
  ```sh
  ps aux
  ```
- **Try Installing Software:**
  ```sh
  apt install netcat
  ```
- **Access Sensitive Files:**
  ```sh
  cat /etc/passwd
  ```

To exit, type:
```sh
exit
```

### Check Logged Activities
```sh
tail -f ~/cowrie/var/log/cowrie/cowrie.log
```

### Show All Entered Passwords
```sh
cat ~/cowrie/var/log/cowrie/cowrie.log | grep "login attempt"
```

### View Sessions Data
```sh
cat ~/cowrie/var/log/cowrie/cowrie.log | grep "New connection"
```
These commands help analyze attack patterns and log details effectively.


## 📧 Contact
For any queries or contributions, feel free to create an issue or reach out!

### 🛑 Disclaimer
**This project is for educational and research purposes only. Use responsibly.**

