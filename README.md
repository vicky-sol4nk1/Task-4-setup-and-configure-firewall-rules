# Task-4-setup-and-configure-firewall-rules
setup and configure firewall rules on linux machine using ufw filrewall

UFW:Uncomplicated Firewall (UFW) is a user-friendly firewall management tool used in Linux systems, especially Ubuntu, to control incoming and outgoing network traffic. It acts as a frontend for iptables, allowing users to create and manage firewall rules using simple and easy-to-understand commands instead of complex configurations. UFW helps secure a system by filtering traffic based on ports, IP addresses, and protocols such as TCP and UDP. It supports both IPv4 and IPv6, allows setting default security policies (like denying all incoming connections), provides logging features for monitoring traffic, and includes predefined application profiles for common services like SSH and web servers. Overall, UFW makes firewall configuration simple while maintaining strong network security.



Great 👍 since you’re using **Linux with UFW**, here’s a complete step-by-step guide you can directly use for your task report.

We’ll assume you’re using **Uncomplicated Firewall (UFW)** on Ubuntu/Kali.

---

# 🔥 Task 4: Setup and Use a Firewall on Linux (UFW)

## ✅ Step 1: Check if UFW is Installed

```bash
sudo ufw status
```

If not installed:

```bash
sudo apt install ufw
```

Enable UFW:

```bash
sudo ufw enable
```

---

## ✅ Step 2: List Current Firewall Rules

```bash
sudo ufw status verbose
```

or numbered list:

```bash
sudo ufw status numbered
```

This shows:

* Active status
* Default policies
* Allowed/blocked ports

---

## ✅ Step 3: Block Inbound Traffic on Port 23 (Telnet)

Port **23** is used for Telnet (insecure protocol).

Add rule:

```bash
sudo ufw deny 23
```

Check again:

```bash
sudo ufw status numbered
```

You should see:

```
23 DENY Anywhere
```

---

## ✅ Step 4: Test the Rule

### 🔹 Local Test:

Install telnet if not installed:

```bash
sudo apt install telnet
```

Try connecting:

```bash
telnet localhost 23
```

Expected Result:
Connection should fail (blocked by firewall).

### 🔹 Remote Test (From another machine):

```bash
telnet <your-ip> 23
```

Connection should timeout or refuse.

---

## ✅ Step 5: Allow SSH (Port 22)

If you're on Linux and using SSH, allow port 22:

```bash
sudo ufw allow 22
```

OR

```bash
sudo ufw allow ssh
```

Check status:

```bash
sudo ufw status
```

You should see:

```
22 ALLOW Anywhere
```

⚠️ Important: Always allow SSH before enabling firewall on remote server, otherwise you may lock yourself out.

---

## ✅ Step 6: Remove the Test Block Rule (Restore State)

First check rule number:

```bash
sudo ufw status numbered
```

Example output:

```
[ 1] 23 DENY Anywhere
```

Delete rule:

```bash
sudo ufw delete 1
```

OR directly:

```bash
sudo ufw delete deny 23
```

Verify again:

```bash
sudo ufw status
```

Port 23 rule should be removed.

---

# 📄 Documentation Summary (You Can Submit This)

### Commands Used:

* `sudo ufw enable`
* `sudo ufw status verbose`
* `sudo ufw deny 23`
* `ssh username@ip`
* `sudo ufw allow 22`
* `sudo ufw delete deny 23`

---

# 🔐 How Firewall Filters Traffic (Concept Explanation)

A firewall works as a **network traffic filter**.

It checks:

* Source IP
* Destination IP
* Port number
* Protocol (TCP/UDP)

### 🔹 How UFW Filters Traffic:

1. Incoming packet arrives.
2. Firewall checks rules from top to bottom.
3. If rule matches → Action taken (ALLOW / DENY).
4. If no rule matches → Default policy applies.

Example:

* If rule says **deny port 23**, all traffic targeting port 23 is blocked.
* If rule says **allow port 22**, SSH traffic is permitted.

 📄 Viva-ready short answers
* 🧠 Interview explanation version

Tell me which one you need 👍
