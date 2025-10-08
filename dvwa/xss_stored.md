In the given field, you simply have to add a script- this script runs whenever you work on something .

on DVWA to be precise, you have to make sure you add the script (add a console.log, that's less annoying), in the bigger field

Stored XSS: Instead of being reflected immediately, the malicious script is saved on the server's database or file system.

Think of it like this:

An attacker posts a comment on a blog. But in the comment, they sneak in a malicious script. The server, being naive, just saves that script along with all the other comments. Now, every time someone visits that blog post and the comments are loaded, the server sends the attacker's script to their browser. The browser runs it, thinking it's part of the website's content.

So, it's "stored" because it's **saved on the server** and is persistent, affecting every user who views that content.