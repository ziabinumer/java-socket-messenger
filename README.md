# Java Socket Messenger

[![Language](https://img.shields.io/badge/Language-Java_17+-ED8B00?logo=openjdk&logoColor=white)](https://www.java.com/)
[![Architecture](https://img.shields.io/badge/Architecture-Client--Server-blue)](#architecture)
[![Concurrency](https://img.shields.io/badge/Concurrency-Multithreaded-success)](#concurrency--networking)
[![License](https://img.shields.io/badge/License-MIT-lightgrey.svg)](LICENSE)

A modular, multi-threaded Java messaging and chat platform built from the ground up using raw TCP sockets (`java.net.Socket`), multithreading, and an object-oriented domain architecture.

---

## ðŸŒŸ Key Features

* **TCP Socket Networking**: Pure socket-based communication between clients and a central server without external messaging libraries.
* **Concurrent Client Handling**: Uses multi-threaded `ClientHandler` threads to manage multiple concurrent client sessions independently.
* **User Authentication**: Built-in authentication service with credential validation and session registration.
* **Presence & Profile Management**: Real-time status tracking (`ONLINE`, `AWAY`, `OFFLINE`) and user profile management.
* **Messaging & File Transfer**: Extensible message hierarchy supporting both direct text messages (`TextMessage`) and binary file transfers (`FileMessage`).
* **Friendship Network**: Maintain friend lists and friendship request management (`FriendManager`).
* **Data Persistence**: Dedicated storage layer (`UserStore`, `ProfileStore`, `FileStorage`) for persistent chat and account state.

---

## ðŸ—ï¸ Architecture

```mermaid
graph TD
    Client1[Java Client A] <-->|TCP Socket:5000| Server[ServerMain / ServerSocketManager]
    Client2[Java Client B] <-->|TCP Socket:5000| Server
    Server --> Registry[SessionRegistry]
    Server --> Handlers[ClientHandler Pool]
    Handlers --> Auth[AuthService]
    Handlers --> Msg[Messaging Service]
    Handlers --> Friends[FriendManager]
    Handlers --> Storage[Storage Layer: UserStore / ProfileStore]
```

---

## ðŸ“ Project Structure

```text
java-socket-messenger/
â”œâ”€â”€ auth/                 # Authentication services & credential validation
â”‚   â”œâ”€â”€ AuthService.java
â”‚   â”œâ”€â”€ AuthValidator.java
â”‚   â””â”€â”€ UserCredentials.java
â”œâ”€â”€ client/               # Client-side connection & I/O dispatchers
â”‚   â”œâ”€â”€ ClientMain.java
â”‚   â”œâ”€â”€ ClientSocket.java
â”‚   â”œâ”€â”€ InputReader.java
â”‚   â””â”€â”€ OutputWriter.java
â”œâ”€â”€ friends/              # Friendship relations and request handling
â”‚   â”œâ”€â”€ FriendList.java
â”‚   â””â”€â”€ FriendManager.java
â”œâ”€â”€ messaging/            # Polymorphic message contracts and handlers
â”‚   â”œâ”€â”€ FileMessage.java
â”‚   â”œâ”€â”€ Message.java
â”‚   â”œâ”€â”€ MessageType.java
â”‚   â””â”€â”€ TextMessage.java
â”œâ”€â”€ profile/              # User metadata and presence tracking
â”‚   â”œâ”€â”€ PresenceStatus.java
â”‚   â”œâ”€â”€ ProfileService.java
â”‚   â””â”€â”€ UserProfile.java
â”œâ”€â”€ server/               # Multi-threaded server daemon & socket loops
â”‚   â”œâ”€â”€ ClientHandler.java
â”‚   â”œâ”€â”€ ServerConfig.java
â”‚   â”œâ”€â”€ ServerMain.java
â”‚   â”œâ”€â”€ ServerSocketManager.java
â”‚   â””â”€â”€ SessionRegistry.java
â”œâ”€â”€ storage/              # File and record persistence engines
â”‚   â”œâ”€â”€ FileStorage.java
â”‚   â”œâ”€â”€ ProfileStore.java
â”‚   â””â”€â”€ UserStore.java
â”œâ”€â”€ Main.java             # Unified application launcher
â””â”€â”€ setup.sh              # Project scaffold script
```

---

## ðŸš€ Getting Started

### Prerequisites
* Java Development Kit (JDK 17 or later recommended)
* `javac` and `java` available on your `PATH`

### 1. Compile the Source
Compile all modules from the project root:

```bash
javac auth/*.java client/*.java friends/*.java messaging/*.java profile/*.java server/*.java storage/*.java Main.java
```

### 2. Start the Server
Launch the central socket server (listens on default port `5000`):

```bash
java server.ServerMain
```
*Console output:*
```text
Server starting on port 5000
```

### 3. Connect a Client
In a separate terminal, launch a client instance:

```bash
java client.ClientMain
```

You can start multiple terminal windows to run concurrent client instances and test multi-user chat sessions.

---

## ðŸ› ï¸ Tech Stack & Design Patterns

* **Language**: Java
* **Networking**: `java.net.ServerSocket`, `java.net.Socket`
* **Concurrency**: Java Threads, Worker Thread per Client Model
* **Patterns Used**:
  * **Facade Pattern**: `AuthService`, `ProfileService`
  * **Polymorphism**: Base `Message` with `TextMessage` & `FileMessage`
  * **Registry Pattern**: `SessionRegistry` for tracking active user channels

---

## ðŸ“„ License

This project is licensed under the MIT License - see the LICENSE file for details.
