### SNMP Enumeration with Nmap and `snmpwalk`

**SNMP** (Simple Network Management Protocol) is a protocol for managing network devices. It uses a "community string" for authentication, which is often set to a default value like `public` or `private`. If these defaults are not changed, an attacker can use them to get a lot of information about the host.

### Nmap

First, use **Nmap** to find if the SNMP service is running on your localhost. SNMP runs on UDP port 161, so you need to tell Nmap to scan for that specific protocol and port.

The command is:

```bash
nmap -sU -p 161 localhost
```

  * `-sU` specifies a UDP scan.
  * `-p 161` specifies the port.
  * `localhost` is the target IP.

If the port is open, Nmap will report it as `open|filtered` or just `open`. You can also use Nmap's scripting engine (NSE) to try and guess the community string.

The command is:

```bash
nmap -sU -p 161 --script snmp-brute localhost
```

if it is closed, (which it probably is) go:
```
systemctl start snmpd.service
systemctl enable snmpd.service
```
snmpd would already be installed, if not, install snmp and snmpd manually

### `snmpwalk`

Once you know SNMP is running and you have a valid community string (like `public`), you can use the `snmpwalk` command to "walk" the entire Management Information Base (MIB) tree and dump all the available information.

The command is:

```bash
snmpwalk -v 2c -c public localhost
```

  * `-v 2c` specifies the SNMP version (a common version with community strings).
  * `-c public` specifies the community string.
  * `localhost` is your target.

This command will output a long list of information, including system description, running processes, network interfaces, and more. This information can be very valuable to an attacker. 🦝