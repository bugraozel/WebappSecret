# Gamenity Architecture Overview

## Vision
Gamenity pairs players based on competitive intensity, chill vibes, and personality preferences. The platform targets quick lobby formation for fast-paced titles (Valorant, LoL, CS2) and relaxed session planning for cozy games (Stardew Valley, Minecraft).

## High-Level System Map
- **Frontend (Next.js 15, TypeScript)**: App Router with server actions, authentication UI, real-time lobby updates via Socket.io client, profile dashboards, community feed.
- **Backend (NestJS 11, TypeScript)**: REST + WebSocket APIs, matchmaking engine, moderation workflows, Prisma-based persistence layer, OAuth integrations.
- **Database (PostgreSQL)**: Normalized domain with JSON columns for flexible preference weights.
- **Messaging & Realtime**: Socket.io handles lobby flow; future work may introduce Redis for scalable pub/sub.

## Domain Modules
- **Identity & Auth**
  - OAuth providers (Google, Discord, Steam) via NestJS Passport strategy.
  - Session tokens using JWT + refresh flow.
- **Profiles**
  - Stores playable titles, roles, time windows, personality toggles.
  - Links to account-level trust score.
- **Matchmaking**
  - Competitive queue: rank, role synergy, behaviour score.
  - Chill queue: session length, chat intent, activity goals.
  - Shadow pool: reroute reported users to hidden queues.
- **Reporting & Moderation**
  - Structured reports, auto flags, admin review queue.
  - Shadow pool assignment rules.
- **Social**
  - Friend graph, direct messages, community timeline.
- **Gamification**
  - Badge emission, seasonal ladders, achievements.

## Data Model Sketch
```
User
  id, email, oauthProvider, oauthId, createdAt, status
Profile
  id, userId (FK), displayName, bio, timezone, voiceOptIn, chillLevel
GamePreference
  id, profileId (FK), gameId, queueType (competitive|chill), roles[], rank, tags
MatchPreference
  id, profileId (FK), availability JSONB, personality JSONB, intensityScore
MatchSession
  id, type (competitive|chill), status, createdAt
MatchParticipant
  id, sessionId (FK), userId (FK), role, ratingSnapshot
Report
  id, reporterId, targetId, reason, severity, status, createdAt
ShadowFlag
  id, userId (FK), score, expiresAt
Friendship
  id, requesterId, addresseeId, status
Message
  id, threadId, senderId, content, createdAt
```

## Iteration Plan
1. **MVP Foundations**
   - Auth placeholder (email magic link or mock until OAuth ready).
   - Profile creation form, matchmaking preference capture.
   - Lobby creation & matchmaking simulation with Socket.io.
   - Basic reporting flow storing reports + assigning shadow pool flag.
2. **Enhancements**
   - OAuth providers, trust scores, admin moderation dashboard.
   - Gamification badges, friend requests, messaging.
3. **Scale & Ops**
   - Redis queue for matchmaking, analytics pipeline, observability stack.

## Tech Decisions
- **Package Management**: npm workspaces to coordinate frontend and backend.
- **Styling**: Tailwind optional; initial pass with CSS Modules/utility classes.
- **Testing**: Playwright + Vitest on frontend, Jest + Pact for backend.
- **CI/CD**: GitHub Actions pipeline (lint, test, build).

## Immediate Next Steps
1. Wire up shared ESLint/Prettier configuration at root.
2. Integrate Prisma with NestJS; create initial schema & migrations.
3. Implement matchmaking module skeleton (controllers, services, gateway).
4. Replace Next.js starter page with product-oriented landing.
5. Establish `.env.example` for both apps.
