# Client Session State

> Stores session state on the client

* How It Works
* When to Use It

## How It Works

* The client sends the full set of session data with each request and the server sends back the full session state with each response. **This allows the server to be completely stateless**.

* Most of the time you'll want to use *Data Transfer Objects* to handle the data transfer.

* With an HTML interface, there are three common ways to do client session state:
  * URL parameters
  * Hidden fields
  * Cookies

* Some platforms can detect whether cookies are enabled; and if not, tey can use URL rewriting.

## When to Use It

* It reacts well in **supporting stateless server objects with maximal clustering and failover resiliency**.

* You almost always have to use *Client Session State* for **session identification**. This should be just one number, but you should still be concerned about **session stealing**, whichi s what happens when a malicious user changes his session ID to see if he can snag someone else's session. Most platforms come up with a random session ID or run it through a hash.

* With large amounts of data the issues of where to store the data and the time cost of transferring everything with every request becomes prohibitive.

* **Security issue**: Any data sent to the client is vulnerable to being looked at and altered. Encryption is the only way to stop this, but encrypting and decrypting with each request is a performance burden. Don't assume that what got sent out is the same as what gets sent back. Any data coming back will need to be completely revalidated.
