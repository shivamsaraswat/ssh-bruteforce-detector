To prevent SSH brute force attacks on a Linux machine:

1). Install the `fail2ban` package using your package manager. This package provides tools for blocking IP addresses that make repeated failed login attempts. (Fail2ban is an intrusion prevention software framework.)

2). Create a configuration file for `fail2ban` in the `/etc/fail2ban` directory. You can use the `sshd` configuration file as a template, and customize it to specify the number of failed login attempts allowed before an IP address is blocked, and the length of time that the IP address should be blocked for.

3). Start the `fail2ban` service using the `systemctl` command. You can use the following command to start `fail2ban` and enable it to start automatically at boot:

```
sudo systemctl start fail2ban
sudo systemctl enable fail2ban
```

4). Test the configuration by attempting to log in to the machine using an incorrect password. The IP address should be blocked after a certain number of failed login attempts.

5). If you need to unblock an IP address that has been banned by `fail2ban`, you can use the `fail2ban-client` command. For example, to unblock an IP address that has been banned by the `sshd` jail, you can use the following command:

```
fail2ban-client unban ssh IP_ADDRESS
```

You can also create a script that automates this process, by prompting the user for an IP address and using the `fail2ban-client` command to unban it. Here's an example of how this might look in code:

```
import subprocess

def unban_ip(ip_address):
    """
    Unban an IP address that has been banned by fail2ban.
    """
    subprocess.run(["fail2ban-client", "unban", "ssh", ip_address])

if __name__ == "__main__":
    ip_address = input("Enter the IP address to unban: ")
    unban_ip(ip_address)
```
