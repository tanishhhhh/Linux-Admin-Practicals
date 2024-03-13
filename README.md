# Linux-Admin-Practicals
Certainly! Here's the content formatted as a `README.md` file for GitHub:

```markdown
# Configure SSH Server for Password Authentication on RHEL 6

To configure SSH server on a remote server running RHEL 6 to allow password authentication, follow these steps:

1. **Install SSH Server**:
   If SSH server is not already installed, you can install it using the following command:
   ```bash
   sudo yum install openssh-server
   ```

2. **Enable SSH Service**:
   Start and enable the SSH service so that it starts automatically upon system boot:
   ```bash
   sudo service sshd start
   sudo chkconfig sshd on
   ```

3. **Edit SSH Configuration File**:
   Open the SSH configuration file `/etc/ssh/sshd_config` in a text editor such as `vi` or `nano`:
   ```bash
   sudo vi /etc/ssh/sshd_config
   ```

4. **Allow Password Authentication**:
   Find the line that begins with `PasswordAuthentication` and make sure it is set to `yes`. If it's commented out (with a `#`), remove the `#`:
   ```bash
   PasswordAuthentication yes
   ```

5. **Save and Close the File**:
   After making the changes, save and close the file.

6. **Restart SSH Service**:
   Restart the SSH service for the changes to take effect:
   ```bash
   sudo service sshd restart
   ```

7. **Firewall Configuration (if applicable)**:
   If you're using a firewall such as iptables or firewalld, make sure to allow SSH traffic (port 22) through the firewall:
   - For iptables:
     ```bash
     sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
     sudo service iptables save
     ```
   - For firewalld:
     ```bash
     sudo firewall-cmd --zone=public --add-port=22/tcp --permanent
     sudo firewall-cmd --reload
     ```

Once you've completed these steps, your SSH server should be configured to allow password authentication. You can now use an SSH client to connect to the server using the server's IP address or hostname, along with the username and password.
```

You can copy and paste this content into a `README.md` file in your GitHub repository to provide instructions on configuring SSH server for password authentication on RHEL 6.
