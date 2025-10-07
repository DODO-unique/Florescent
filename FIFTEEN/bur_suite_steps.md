### Step-by-Step: Brute-Forcing DVWA with Burp Intruder

#### **Step 1: Set up Burp Suite Proxy**

1.  Open Burp Suite.
2.  Go to the **Proxy** tab.
3.  Ensure "Intercept is on" (the button should say "Intercept is on").
4.  click the 'open browser button'

#### **Step 2: Capture the Login Request**

1.  In your browser, go to the DVWA login page (`http://localhost/DVWA/login.php`).
2.  on burp suite, you will see a request, click 'forward' to load the site
3.  Enter a fake username and password (e.g., `user` and `pass`).
4.  Click the "Login" button.
5.  Immediately go back to Burp Suite (if it doesn't open automatically). You should see the HTTP request for the login page captured in the **Proxy** tab.

#### **Step 3: Send to Intruder**

1.  In Burp Suite's Proxy tab, find the captured login request. It will be a `POST` request to `login.php`.
2.  Right-click on the request.
3.  From the context menu, select **"Send to Intruder"**.

#### **Step 4: Configure Intruder**

1.  Go to the **Intruder** tab.
2.  Go to the **Positions** sub-tab.
3.  Click the "Clear §" button to clear any pre-selected positions.
4.  Highlight the value of the username parameter (e.g., `user`).
5.  Click the **"Add §"** button. This marks the username as a payload position.
6.  Highlight the value of the password parameter (e.g., `pass`).
7.  Click the **"Add §"** button. This marks the password as the second payload position.
8.  The attack type should be set to **"Cluster Bomb"**. This is crucial, as it tries every combination of usernames and passwords from two different lists.

#### **Step 5: Load Your Payloads (the Wordlists)**

1.  Go to the **Payloads** sub-tab.
2.  In the "Payload set" dropdown, ensure it says **1**. This is for the username.
3.  Under "Payload Options [Simple list]", paste a list of usernames. For DVWA, common usernames are `admin`, `guest`, `user`, etc. A simple list would be:
    ```
    admin
    guest
    user
    ```
4.  Change the "Payload set" dropdown to **2**. This is for the password.
5.  Under "Payload Options [Simple list]", paste a list of passwords. A common list for testing would be:
    ```
    password
    123456
    guest
    ```
6.  *Optional but helpful*: Go to the **Options** tab. Under "Grep - Extract," you can add a rule to look for a specific string in the response. For a successful login, the response body might contain "Welcome," or the URL might redirect to `/vulnerabilities/`. Adding this can help you quickly spot the successful attempt.

#### **Step 6: Start the Attack & Analyze Results**

1.  Click the **"Start attack"** button at the top right.
2.  A new window will open showing the attack's progress.
3.  Watch the "Length" column in the results table. A failed login will usually have a consistent response length, while a **successful login will often have a different, longer or shorter response length** because it's a redirect to the next page.
4.  Alternatively, if you added the "Grep - Extract" rule, you'll see a column with a checkmark for the successful login.
5.  When you find a row with a different length, click on it and look at the "Response" tab to confirm you've found the correct credentials. For DVWA, the credentials are `admin` and `password`.

You got this. Breathe, focus, and let me know if you hit a snag. Good luck\! 