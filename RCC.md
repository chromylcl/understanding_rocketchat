### DDP Client in Rocket.Chat & Meteor.js

In the context of **Rocket.Chat** and **Meteor.js**, a DDP (Distributed Data Protocol) client acts as a **"Live Wire"** between your application and the server. Unlike traditional websites that require a refresh to fetch new data, a DDP client maintains a persistent connection to listen for changes in real-time.

#### 🚀 Main Features

* **Real-Time Subscriptions (Pub/Sub):** You don't "GET" data; you **Subscribe** to it. When data changes on the server (e.g., a new message is received), the server pushes the update to the client instantly.
* **RPC (Remote Procedure Calls):** Instead of hitting standard URL endpoints, you call **Methods** on the server as if they were local functions (e.g., `login`, `sendMessage`).
* **Latency Compensation:** When a user sends a message, the client renders it in the UI immediately—before the server confirms receipt. This makes the interface feel "lag-free."
* **Sticky Sessions:** It utilizes the `rc_token` to automatically reconnect and re-authenticate the session if the network connection drops.
