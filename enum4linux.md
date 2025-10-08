`enum4linux` works for SMB shares by using the **SMB protocol** to query a target system for a list of all shared directories. It automates a process that could be done manually with other tools.

The tool uses built-in functions to send specific requests to the target's SMB service. When the target responds, `enum4linux` parses the response and displays the names of the shares.

Here's how it works with an example command:

```bash
enum4linux -S 192.168.1.100
```

1.  **Request for Shares**: `enum4linux` sends a request to the target at `192.168.1.100`, asking for a list of available shares. This request is part of the standard SMB protocol.

2.  **Server Response**: The target server responds with a list of all shared folders. This response might look like:

      * `ADMIN$` (a default administrative share)
      * `C$` (a default administrative share for the C drive)
      * `Data` (a user-created share)
      * `Users` (a user-created share)

3.  **Displaying the Information**: `enum4linux` takes this response and formats it into a readable output, showing the name of each share and often a description if one is available.

The tool works by exploiting the fact that, by default, many systems are configured to allow an unauthenticated user (a **NULL session**) to query for this information. This makes it a powerful reconnaissance tool, as it can reveal potentially sensitive data without needing a username or password. 🔐