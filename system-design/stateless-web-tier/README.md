# Stateless Web Tier

For scaling the web tier horizontally, we need to **move the state (e.g., user session data) out of the web tier**. A good practice is to store session data in the persistent storage so that each web server in the cluster can access state data from databases. This is called stateless web tier.

In a stateless architecture, **HTTP requests from users can be sent to any web servers**, which fetch state data from a shared data store that is kept out of web servers. This approach is simpler, **more robust and scalable**.
