# Cookbook: Building a Web Service

This recipe demonstrates how to build a secure, isolated HTTP server using the Exosphere Rust SDK.

## 🥣 Ingredients

-   **`net.tcp_listen:8080`**: Permission to bind to a local port.
-   **`net.tcp_write`**: Permission to send data over a socket.
-   **`io.print`**: For logging status.

---

## 👨‍🍳 Implementation (Rust)

```rust
use crush_sdk::{Capsule, Manifest, Result, capsule_main, net, io};

struct WebServer;

impl Capsule for WebServer {
    fn run(&mut self, entry_point: &str) -> Result<()> {
        io::print("Starting web server on port 8080...")?;
        
        let listener = net::tcp_listen(8080)?;
        
        loop {
            let (mut stream, addr) = listener.accept()?;
            io::print(&format!("Accepted connection from: {}", addr))?;
            
            let response = "HTTP/1.1 200 OK\r\nContent-Length: 21\r\n\r\nHello from Exosphere!";
            stream.write_all(response.as_bytes())?;
        }
    }
}

capsule_main!(WebServer);
```

---

## 📝 The Manifest (`Capsule.toml`)

To run this server, you must explicitly grant the `net.tcp_listen` capability.

```toml
[capsule]
name = "secure-web-srv"
version = "0.1.0"

[permissions]
required = ["net.tcp_listen", "io.print"]
scopes = ["net.tcp_listen:8080"]
```

## 🛡️ Why this is "Exosphere-Safe"

In a traditional OS, if your web server has a vulnerability (e.g., Buffer Overflow), the attacker might gain shell access to your entire user account.

In Exosphere:
1.  **Port Restricted**: The server can *only* listen on port 8080. It cannot pivot to scan internal ports.
2.  **No Shell**: There is no ambient shell available to the attacker. They are trapped in the CASM execution sandbox.
3.  **VFS Locked**: The attacker cannot read `/etc/passwd` or ssh keys because the VFS root is empty or strictly scoped to a dedicated web directory.
