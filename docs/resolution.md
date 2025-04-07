# Errors Encountered and Resolutions

If you see the error:

```
Failed to restart sshd.service: Unit sshd.service not found.
```

It means that the `sshd` service is either not installed, running under a different name, or not enabled. Here’s how to troubleshoot:

---

### **1. Check If SSH is Installed**

Run:

```sh
which sshd
```

If SSH is installed, this should return a path like `/usr/sbin/sshd`. If nothing appears, install OpenSSH:

- **Debian/Ubuntu**:

  ```sh
  sudo apt update && sudo apt install openssh-server -y
  ```

- **RHEL/CentOS**:

  ```sh
  sudo yum install openssh-server -y
  ```

- **Arch Linux**:

  ```sh
  sudo pacman -S openssh
  ```

---

### **2. Check the Correct Service Name**

On some systems, the SSH service might be named differently. Try:

```sh
sudo systemctl list-units --type=service | grep ssh
```

If you see `ssh.service` instead of `sshd.service`, restart it using:

```sh
sudo systemctl restart ssh
```

---

### **3. Start & Enable SSH Service**

If SSH is installed but not running:

```sh
sudo systemctl start ssh
sudo systemctl enable ssh
```

For RHEL-based systems:

```sh
sudo systemctl start sshd
sudo systemctl enable sshd
```

---

### **4. Check SSH Status**

To confirm it's running:

```sh
sudo systemctl status ssh
```

or

```sh
sudo systemctl status sshd
```

---

<!-- trunk-ignore(markdownlint/MD047) -->
Let me know which distro you're using if this doesn't solve it! 🚀
