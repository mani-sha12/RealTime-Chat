# Real-time Chat App

> Rooms, private messages, online status and typing indicators

**Level:** Intermediate  |  **Estimated time:** 1 to 2 weeks

## Overview

A WhatsApp or Slack-style chat that teaches WebSockets, event-driven design and message persistence.

## Screenshots

_Add screenshots or a GIF here once the UI works._

**Live demo:** _add link after deploying_

## Features

- Register and login
- Public chat rooms and create your own room
- One-to-one private messages
- Online and offline status
- Typing indicator
- Message history loaded with pagination
- Unread message counts
- Emoji picker and image sharing
- Read receipts

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React, Socket.IO client, Tailwind CSS |
| Backend | Node.js, Express, Socket.IO |
| Database | MongoDB with Mongoose |
| Auth | JWT (also verified during the socket handshake) |

## Getting Started

### Prerequisites

- Node.js 20+
- Git
- A database as described in the tech stack

```bash
git clone https://github.com/YOUR-USERNAME/realtime-chat.git
cd realtime-chat

cp server/.env.example server/.env   # then fill in the values

# Database
MongoDB needs no migration. Point MONGODB_URI at a local MongoDB or a free MongoDB Atlas cluster.

# Backend
cd server
npm install
npm run dev

# Frontend (new terminal)
cd client
npm install
npm run dev
```

### First-time scaffolding

This repository is a **starter skeleton**: folders and placeholder files are ready, but you still need to create the app itself.

```bash
cd server && npm init -y     # then install the packages your stack needs, e.g. express, cors, dotenv
cd ../client && npm create vite@latest . -- --template react
```

## Project Structure

```
realtime-chat/
  client/src/
    socket.js
    components/  Sidebar.jsx  ChatWindow.jsx  MessageBubble.jsx  TypingIndicator.jsx
    pages/  Login.jsx  Chat.jsx
  server/src/
    models/  User.js  Room.js  Message.js
    routes/  auth.js  rooms.js  messages.js
    sockets/  index.js  chatHandlers.js  presence.js
```

## Data Model

| Entity | Fields |
|---|---|
| User | id, username, email, passwordHash, avatar, lastSeen |
| Room | id, name, isPrivate, members[], createdBy |
| Message | id, room, sender, text, imageUrl, readBy[], createdAt |

## API Endpoints

| Method | Route | Purpose |
|---|---|---|
| POST | `/api/auth/login` | Login |
| GET | `/api/rooms` | Rooms for the user |
| POST | `/api/rooms` | Create room |
| GET | `/api/rooms/:id/messages` | Paginated history |
| SOCKET | `join_room / leave_room` | Enter or leave a room |
| SOCKET | `send_message` | Broadcast and save message |
| SOCKET | `typing / stop_typing` | Typing indicator events |
| SOCKET | `user_online / user_offline` | Presence updates |

## Roadmap

**Phase 1: REST and auth**

- [ ] User model, login, rooms and messages endpoints

**Phase 2: Sockets**

- [ ] Authenticate socket connection with JWT
- [ ] Join rooms, send and receive messages, save to database

**Phase 3: Presence and typing**

- [ ] Track connected users in a Map, broadcast status
- [ ] Typing events with debounce

**Phase 4: UI polish**

- [ ] Auto-scroll, unread badges, emoji picker
- [ ] Deploy backend with WebSocket support

## Stretch Goals

- [ ] Redis adapter to scale across servers
- [ ] Message editing and deletion
- [ ] Voice notes
- [ ] Push notifications
- [ ] End-to-end encryption demo

## Deployment

Backend on Render or Railway (both support WebSockets), frontend on Vercel, database on MongoDB Atlas. Serverless platforms are not suitable for the socket server.

## Full Blueprint

A detailed planning document is in [`docs/`](docs/).

## Push to GitHub

```bash
git init
git add .
git commit -m "feat: initial project setup"
gh repo create realtime-chat --public --source=. --remote=origin --push
```

Suggested repository topics: `react`, `socketio`, `websocket`, `mongodb`, `chat-app`, `realtime`

## License

MIT. See [LICENSE](LICENSE).
