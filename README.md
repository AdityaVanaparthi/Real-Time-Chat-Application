# Real-Time Chat Application

A real-time messaging web application built using **Spring Boot and WebSockets**. It allows users to send and receive messages instantly without refreshing the page.

## Features

- **Real-time messaging:** Send and receive messages instantly.
- **WebSocket communication:** Enables continuous, bidirectional communication between the client and server.
- **STOMP messaging:** Handles message destinations and subscriptions.
- **SockJS support:** Provides a fallback mechanism for WebSocket communication.
- **Simple chat interface:** Built using HTML, CSS, and Bootstrap.
- **Spring Boot backend:** Handles incoming messages and broadcasts them to connected subscribers.
- **No database required:** Messages are exchanged in real time and are not persisted by the current implementation.

## Tech Stack

| Technology | Purpose |
|---|---|
| Java 21 | Programming language |
| Spring Boot 4.1.1 | Backend application framework |
| Spring WebSocket | Real-time communication |
| STOMP | Messaging protocol |
| SockJS | WebSocket fallback support |
| Thymeleaf | Server-side page rendering |
| HTML and CSS | Frontend structure and styling |
| Bootstrap 5 | Responsive UI components |
| Maven | Dependency management and build tool |
| Lombok | Reduces boilerplate Java code |

## Project Structure

```text
app/
├── src/
│   ├── main/
│   │   ├── java/com/chat/app/
│   │   │   ├── AppApplication.java
│   │   │   ├── config/
│   │   │   │   └── WebSocketConfig.java
│   │   │   ├── controller/
│   │   │   │   └── ChatController.java
│   │   │   └── model/
│   │   │       └── ChatMessage.java
│   │   └── resources/
│   │       ├── application.properties
│   │       └── templates/
│   │           └── chat.html
│   └── test/
│       └── java/com/chat/app/
│           └── AppApplicationTests.java
├── pom.xml
├── mvnw
└── mvnw.cmd
```

## How It Works

1. The user opens the chat page and connects to the `/chat` SockJS endpoint.
2. The frontend subscribes to `/topic/messages` to receive messages.
3. When a user sends a message, the frontend publishes it to `/app/sendMessage`.
4. The `ChatController` receives the message through the `@MessageMapping("/sendMessage")` method.
5. The `@SendTo("/topic/messages")` annotation broadcasts the message to subscribers.
6. The frontend displays the sender's name and message content in the chat window.

## Prerequisites

- Java Development Kit (JDK) 21 or compatible setup
- Git
- An IDE such as IntelliJ IDEA or VS Code
- Internet connection for downloading Maven dependencies and frontend libraries

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/chat-app.git
cd chat-app/app
```

Replace `YOUR_USERNAME` with your GitHub username and use the actual repository name if different.

### 2. Run the application

**Windows PowerShell:**

```powershell
.\mvnw.cmd spring-boot:run
```

**Linux/macOS:**

```bash
./mvnw spring-boot:run
```

Alternatively, open the project in IntelliJ IDEA and run `AppApplication.java`.

### 3. Open the chat application

Visit:

```text
http://localhost:8080/chat
```

The default Spring Boot port is `8080`, unless changed in `application.properties`.

### 4. Test real-time messaging

1. Open the chat page in two browser tabs.
2. Enter a sender name in each tab.
3. Type a message and click **Send**.
4. Verify that the message appears in both tabs.

## Key Components

### `ChatMessage.java`

Represents a chat message with the following fields:

- `id` — message identifier
- `sender` — name of the sender
- `content` — message content

Lombok generates getters, setters, and other common methods.

### `ChatController.java`

Handles the incoming messages and broadcasts them to subscribers. It also maps the `/chat` HTTP route to the Thymeleaf `chat.html` template.

### `WebSocketConfig.java`

Configures the STOMP endpoint, enables SockJS, registers the `/topic` message broker, and sets `/app` as the application destination prefix.

### `chat.html`

Provides the chat interface and uses JavaScript, SockJS, and STOMP to establish the connection, send messages, and update the chat window.

## Current Limitations

- Messages are not saved in a database.
- User authentication and authorization are not implemented.
- Message history is not available after messages have been missed or the application restarts.
- The current application uses Spring's simple in-memory message broker.

## Future Enhancements

- Add user authentication and private messaging.
- Store chat messages using MySQL or MongoDB.
- Display online users and typing indicators.
- Add chat rooms and group conversations.
- Improve the interface for mobile devices.
- Add message timestamps and delivery indicators.

## License

This project is available for learning and personal development. Add a specific open-source license if you intend to distribute it under defined reuse terms.
