# Low-Level HTTP Server

> A fully functional HTTP/1.1 server built from scratch in C++98.

A robust, non-blocking HTTP server that handles real-world web traffic, including static content delivery, dynamic scripting via CGI, virtual hosts, and secure configuration. Designed to be resilient, scalable, and compliant with modern web standards — all implemented without external libraries.

This project demonstrates deep understanding of **network programming**, **protocol design**, and **system-level C++**.

---

### 🛠️ Features

#### 🔹 **Core HTTP Server**
- Implements **HTTP/1.1 protocol** with support for:
  - `GET`, `POST`, `DELETE` methods
  - Chunked transfer encoding
  - Persistent connections
- Built in **C++98** with no external dependencies
- **Non-blocking I/O** using `epoll` (Linux) / `kqueue` (macOS) for high concurrency with a single thread
- Handles **graceful client disconnections** and timeouts
- Never crashes — designed for resilience under edge cases

#### 🔹 **Configuration & Virtual Hosting**
- Parses a **NGINX-style configuration file** to define multiple server blocks
- Supports:
  - Multiple **ports** and **server names**
  - Custom **error pages** (`404`, `403`, `500`, etc.)
  - **Directory listing** with auto-indexing
  - **Root** and **alias** directives for file path mapping
  - **Client max body size** limits
- Enables **virtual hosting**: serve different websites from the same server

#### 🔹 **Dynamic Content with CGI**
- Executes external scripts via **CGI (Common Gateway Interface)**
- Supports **PHP-CGI** for dynamic content generation
- Manages process lifecycle with `fork()` and `execve()`
- Pipes data between server and script via `stdin`/`stdout`
- Configurable per-location CGI execution

#### 🔹 **Security & Access Control**
- **Location-based access control**: restrict HTTP methods (`GET`, `POST`, etc.)
- **Authentication support**: basic HTTP auth placeholder (can be extended)
- Prevents directory traversal attacks (e.g., `../../../etc/passwd`)
- Sanitizes all inputs and validates paths

#### 🔹 **Advanced Networking & Performance**
- **Upload handling**: accepts file uploads via `POST` requests
- **Redirections**: supports `301`, `302`, `307`, `308` redirects
- **Auto-redirect**: appends `/` to directories when missing
- **Server header masking**: customizable or hidden `Server` field
- **Keep-alive support**: efficient reuse of TCP connections

#### 🔹 **Session & State Management**
- **Cookie parsing and generation** for session tracking
- Can be extended to support full **session management**
- Logs session activity for debugging

#### 🔹 **Extensibility & Maintainability**
- Modular architecture: each feature is isolated and configurable
- Clean, norm-compliant C++98 codebase
- No memory leaks (verified with `valgrind`)
- Fully self-contained: no use of `std::tr1`, `boost`, or other forbidden libraries

---

### 🧰 Tech Stack
- **Language**: C++98
- **Networking**: `socket`, `bind`, `listen`, `accept`, `send`, `recv`
- **I/O Multiplexing**: `epoll` (Linux), `kqueue` (macOS), `poll` (fallback)
- **Configuration**: Custom parser for NGINX-like `.conf` files
- **CGI**: `fork`, `execve`, `pipe`, `dup2`
- **Tools**: `Makefile`, `g++`, `valgrind`, `telnet`, `curl`
