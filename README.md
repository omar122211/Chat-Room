# Chat Room in C

A multi-user terminal chat over TCP, written in C. Many clients connect to one server and send **public** messages to everyone or **private** messages to one user — and every message is checked for corruption with a **checksum and a CRC**.

## Features

- **Concurrent clients** — the server gives each client its own POSIX thread (up to 100 clients)
- **Thread-safe** — the shared client list is protected with a mutex
- **Public & private messages** — send to `all` or to a user's name
- **Integrity checks** — the client attaches a checksum and a CRC to each message; the server recomputes both and rejects corrupted messages
- **Active users list** shown when you join
- **Chat log** — each client saves its conversation to a timestamped text file

## How it works

```
client ──TCP──▶ server (one thread per client)
   message = { recipient, text, checksum, CRC }
   server verifies checksum + CRC ──▶ forwards to "all" or to one user
```

## Build & run (Linux / macOS)

```bash
make                 # builds ./server and ./client

./server 8080        # terminal 1: start the server on a port
./client 8080        # terminal 2+: each client enters a name, then chats
```

When sending, type the recipient (`all` for everyone, or a user's name), then the message. Type `exit` to leave.

## Built with

C · TCP sockets · POSIX threads (pthreads) · mutexes
