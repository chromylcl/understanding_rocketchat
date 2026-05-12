### DDP Client in Rocket.Chat & Meteor.js

In the context of **Rocket.Chat** and **Meteor.js**, a DDP (Distributed Data Protocol) client acts as a **"Live Wire"** between your application and the server. Unlike traditional websites that require a refresh to fetch new data, a DDP client maintains a persistent connection to listen for changes in real-time.

#### 🚀 Main Features

* **Real-Time Subscriptions (Pub/Sub):** You don't "GET" data; you **Subscribe** to it. When data changes on the server (e.g., a new message is received), the server pushes the update to the client instantly.
* **RPC (Remote Procedure Calls):** Instead of hitting standard URL endpoints, you call **Methods** on the server as if they were local functions (e.g., `login`, `sendMessage`).
* **Latency Compensation:** When a user sends a message, the client renders it in the UI immediately—before the server confirms receipt. This makes the interface feel "lag-free."
* **Sticky Sessions:** It utilizes the `rc_token` to automatically reconnect and re-authenticate the session if the network connection drops.



### Example Workflow: A Chat App

Here is how the DDP client handles a typical **"User logs in and sends a message"** flow:

#### 1. Connection & Auth
The client connects to the server and checks if you have a stored token.
*   **Action:** `new DDPClient({ host, getToken })`
*   **Result:** WebSocket opens; `getToken` retrieves the `rc_token`.

#### 2. Subscription (The "Listener")
The client tells the server it wants to "watch" a specific room.
*   **Action:** `client.subscribe("stream-room-messages", rid)`
*   **Result:** The server "bookmarks" this client. Whenever a message is added to that Room ID (`rid`) in the database, the server pushes a JSON packet to the client.

#### 3. Method Call (The "Action")
The user types a message and hits send.
*   **Action:** `client.call("sendMessage", { msg: "Hello bro!", rid: "GENERAL" })`
*   **Result:** The server receives the request, validates the user, saves it to MongoDB, and then broadcasts it to all other subscribers.

#### 4. Disconnect & Reconnect
The user goes into a tunnel and loses Wi-Fi.
*   **Action:** WebSocket closes.
*   **Result:** The DDP client automatically tries to reconnect. Once back online, it sends the `rc_token` again and automatically re-subscribes to the room so the user doesn't miss a beat.

