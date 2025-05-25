## 📌 What is a Web Server?

A **Web Server** is a software or hardware system that accepts incoming HTTP/HTTPS requests from clients (usually browsers) and returns responses such as web pages, static files, or data.

### ✅ Key Responsibilities:
- Handling HTTP/HTTPS requests
- Serving static files (HTML, CSS, JS)
- Routing API requests to application logic
- Acting as a reverse proxy or load balancer
- Managing SSL, caching, and logging

---

## 🚀 Popular Web Server Technologies

| Web Server       | Highlights |
|------------------|------------|
| **Apache**        | Most widely used, open-source, highly configurable |
| **Nginx**         | Lightweight, fast, great for static content & reverse proxy |
| **Node.js**       | JavaScript runtime; used with Express/Fastify for dynamic apps |
| **LiteSpeed**     | Fast, drop-in replacement for Apache |
| **Tomcat**        | Java-based server, handles JSP and servlets |
| **Caddy**         | Modern server with auto HTTPS (Let’s Encrypt) |
| **Microsoft IIS** | Native to Windows Server; ideal for .NET apps |

---

## 🧩 Typical Architecture

```plaintext
[ Client (Browser) ]
         │
         ▼
[ Web Server (Nginx/Apache) ]
         │
         ▼
[ Application Server (Node.js, Django, etc.) ]
         │
         ▼
[ Database (PostgreSQL, MongoDB, etc.) ]
