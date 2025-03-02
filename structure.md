# Program Structure: Trading Simulation Game

## Overview
This document outlines the architecture and structure of the trading simulation game built with React (Vite) for the frontend, a Go backend, and a MongoDB database.

## Tech Stack
- **Frontend:** React (Vite)
- **Backend:** Go (Gin/Fiber/Chi, TBD)
- **Database:** MongoDB
- **Real-time Communication:** WebSockets (for live market updates, trades, and game state synchronization)
- **Authentication:** JWT-based auth
- **Hosting & Deployment:** TBD (potentially Vercel for frontend, Fly.io/Heroku for backend, MongoDB Atlas for DB)

## System Architecture
```
[React (Vite) Frontend]  <-- WebSockets/API -->  [Go Backend]  <---> [MongoDB Database]
```
### Components:
- **Frontend:**
  - UI for market visualization, trade execution, player stats
  - WebSocket handling for real-time updates
  - API interactions for authentication and initial data load
- **Backend:**
  - REST API for auth, user management, and initial game state
  - WebSocket server for real-time events (market updates, trades)
  - Game logic (handling trades, market fluctuations, scoring, etc.)
  - Database interactions
- **Database (MongoDB):**
  - Stores user data, game sessions, trade history, market states
  - Optimized for fast lookups of player portfolios and market movements

## Data Flow
1. **Client loads game** → Fetches initial game state via REST API
2. **Client connects to WebSocket** → Listens for market updates & trade events
3. **Player submits a trade** → Sent via WebSocket → Processed by backend
4. **Backend updates game state** → Updates MongoDB → Broadcasts to all players
5. **Player disconnects/reconnects** → Re-authenticates & fetches latest game state

## Core Modules
### Frontend
- `src/components/` – UI components (charts, order forms, dashboards)
- `src/hooks/` – Custom hooks for game state & WebSockets
- `src/services/` – API/WebSocket service handlers
- `src/pages/` – Main game screens

### Backend
- `handlers/` – HTTP & WebSocket handlers
- `models/` – Data models (users, trades, markets)
- `services/` – Business logic (trade execution, scoring, market simulation)
- `routes/` – API route definitions
- `db/` – MongoDB connection & queries

## Deployment
- **Frontend:** Vercel or Netlify
- **Backend:** Fly.io, Railway, or self-hosted VPS
- **Database:** MongoDB Atlas or self-hosted MongoDB instance

## API & Events
### REST API
- `POST /api/auth/login` – Authenticates user
- `GET /api/game/state` – Fetches initial game state
- `POST /api/trade` – Submits a trade (fallback if WebSocket unavailable)

### WebSocket Events
- `market_update` – Broadcasts real-time market price changes
- `trade_executed` – Notifies players when a trade is processed
- `game_state_sync` – Synchronizes game state upon reconnect

---
this document should evolve as the project progresses. add diagrams if needed.

