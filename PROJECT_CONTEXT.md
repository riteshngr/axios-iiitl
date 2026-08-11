# Stitch — Project Context

> **This document is the single source of truth for the Stitch application.**
> Every AI agent and every developer must read this file before making any architectural or design decisions.

---

## 1. Product Vision

**Stitch** is a student-exclusive social and community platform built for IIIT Lucknow (with plans to expand to other institutes).  
It gives students a private, verified space to:

- Connect authentically with peers through a unique slow-connection model (Wonder Chat)
- Participate in official and student-run communities
- Post needs (academic, logistical, social) and get help from the community
- Stay informed via institute announcements
- Build a verified student identity

The guiding philosophy is **genuine connection over viral noise**. Features are intentionally designed to slow down and deepen interactions rather than optimise for engagement metrics.

---

## 2. Platform & Technology

| Concern | Decision |
|---|---|
| Framework | Flutter (Dart) — single codebase |
| Primary targets | Android, iOS |
| Secondary targets | Web (optional, future) |
| Backend | Firebase (planned — not yet integrated) |
| State management | TBD (likely Riverpod or Bloc) |
| Design language | Stitch visual design (see §10) |

---

## 3. Navigation Architecture

### Bottom Navigation Bar (always visible)

```
[ Home ]  [ Community ]  [ Need ]  [ Profile ]
```

| Tab | Purpose |
|---|---|
| **Home** | Personalised feed — posts from joined communities, announcements, trending Needs |
| **Community** | Browse, join, and participate in communities |
| **Need** | Post and browse student Needs |
| **Profile** | Personal profile, settings, activity history |

### Inbox (accessed separately — NOT a bottom tab)

- Reached via an **icon in the top app bar** (e.g. mail/bell icon)
- Contains two sections:
  1. **Direct Messages (DMs)** — standard 1:1 text conversations between connected users
  2. **Wonder Chat** — curated slow-chat connections (see §6)

---

## 4. Authentication & User Identity

- Students register with their **official institute email** (e.g. `@iiitl.ac.in`)
- Email is verified via Firebase Auth
- Each user has a **unique student profile** (see §8)
- Authentication is **not yet implemented** — planned for Phase 2

---

## 5. Home Feed

- Aggregates content from:
  - Communities the user has joined
  - Institute-wide announcements
  - Trending / recent Needs
- Posts are displayed in a Reddit-inspired card layout
- Supports upvote / downvote signals (exact mechanic TBD)
- Users can filter the feed by category

---

## 6. Wonder Chat — Genuine Connection System

Wonder Chat is the flagship differentiator of Stitch.

### Concept

Rather than instantly connecting strangers, Wonder Chat uses a **slow, intentional messaging model**:

1. Two students who don't know each other are placed into a Wonder Chat session.
2. They can exchange messages **one at a time**, with no pressure for instant replies.
3. After **100 genuine, substantive messages** have been exchanged (combined), the connection is considered **established**.
4. At that point, a full DM conversation unlocks between them and they appear in each other's contacts.

### Rules

- The 100-message threshold counts only messages passing a **minimum quality filter** (not empty, not single-character, not copy-pasted spam — exact filter logic TBD).
- Wonder Chat conversations are **private** and never shared or shown publicly.
- A user may have a limited number of active Wonder Chats at once (limit TBD).
- Wonder Chat lives inside **Inbox**, not the bottom navigation.

---

## 7. Community System

### Types of Communities

| Type | Description |
|---|---|
| **Official** | Created and managed by institute administration or verified clubs/societies. Marked with a verified badge. |
| **Student-created** | Any student can apply to create a community. Must be approved before it goes live. |

### Community Approval Workflow

1. Student submits a community creation request (name, description, category, rules).
2. Request enters a **moderation queue** visible to Master Admins.
3. Admin approves or rejects with optional feedback.
4. Approved communities become discoverable and joinable by all students.

### Community Features

- **Posts** — Reddit-style posts (text, images, links) within a community
- **Nested Comments** — threaded comment system (Reddit-style: comment → reply → reply to reply…)
- **Upvote / Downvote** on posts and comments
- **Community Rules** — set by the community creator/moderators
- **Community Roles** — Member, Moderator, Admin (creator)
- **Pinned Posts** — moderators can pin important posts
- **Community Announcements** — official communities can push announcements

---

## 8. Need Feature

The Need feature allows students to post requests for help.

### Need Types (examples — final list TBD)

- Academic (notes, tutoring, study group)
- Logistical (lost & found, transport, accommodation)
- Social (looking for teammates, event buddies)
- Resource (borrow a book, equipment)

### Need Post Structure

- Title
- Description
- Category / tags
- Urgency level (optional)
- Expiry date (optional — Need auto-closes after date)
- Contact preference (DM, comment, phone — user chooses)

### Need Discovery

- Browsable via the **Need** bottom tab
- Filterable by category, urgency, and proximity (future)
- Students can respond by commenting or DMing the poster

---

## 9. Student Profile

Each student has a public-facing profile:

| Field | Notes |
|---|---|
| Display name | Chosen by student |
| Avatar | Uploaded photo or generated avatar |
| Institute | Auto-filled from verified email |
| Year / Branch | Optional, self-reported |
| Bio | Short free-text |
| Communities | Communities the student has joined (can hide) |
| Posts & Needs | Activity history (can hide) |
| Wonder Chat status | Shows if user is open to Wonder Chats |
| Connection count | Number of established Wonder Chat connections |

---

## 10. Announcements

- Institute-wide announcements are posted by **Official accounts** (admin-designated)
- Announcements appear:
  - In the **Home feed** (pinned at top or highlighted)
  - As **push notifications** (future)
- Students cannot post announcements — read-only for regular users

---

## 11. Master Admin Controls

A separate **Admin Panel** (likely web-based, future scope) provides:

| Control | Description |
|---|---|
| User management | Suspend, ban, or reinstate accounts |
| Community approval queue | Approve / reject student community requests |
| Content moderation | Review reported posts, comments, DMs |
| Announcement publishing | Create and schedule institute-wide announcements |
| Platform analytics | User growth, engagement, community health |
| Wonder Chat oversight | Aggregate stats only — individual chats are private |

Master Admin access is restricted to designated institute personnel only.

---

## 12. Moderation

### User-level reporting

- Any user can **report** a post, comment, community, or profile
- Reports go into a moderation queue

### Community-level moderation

- Community Moderators can remove posts/comments within their community
- Community Moderators can ban users from their specific community

### Platform-level moderation

- Master Admins handle escalated reports
- Serious violations (harassment, illegal content) result in account suspension or ban

### Content policies (TBD — to be drafted separately)

---

## 13. Planned Firebase Architecture

> Firebase has **not yet been integrated**. The following is the planned architecture.

| Firebase Service | Planned Use |
|---|---|
| **Firebase Auth** | Email/password + institute email verification |
| **Cloud Firestore** | Primary database — users, communities, posts, comments, Needs, Wonder Chats |
| **Firebase Storage** | Profile photos, post images, community banners |
| **Firebase Cloud Messaging (FCM)** | Push notifications |
| **Firebase Analytics** | Usage analytics (privacy-respecting) |
| **Firebase App Check** | API abuse prevention |

### Firestore Collection Structure (draft)

```
/users/{userId}
/communities/{communityId}
/communities/{communityId}/posts/{postId}
/communities/{communityId}/posts/{postId}/comments/{commentId}
/needs/{needId}
/wonderChats/{chatId}
/wonderChats/{chatId}/messages/{messageId}
/announcements/{announcementId}
/reports/{reportId}
/adminQueue/{queueItemId}
```

### Security Principles

- All Firestore Security Rules must enforce that only authenticated, verified students can read/write data
- No secrets, API keys, or service account credentials are ever committed to Git
- Admin operations require server-side verification (Cloud Functions — future)

---

## 14. UI / Design Direction — Stitch Visual Design

- The app follows the **Stitch design system** established in our Figma/Stitch mockups
- Key characteristics:
  - Clean, minimal layouts with generous whitespace
  - A distinct **primary brand colour palette** (to be defined in the theme file)
  - Rounded cards and components
  - Smooth transitions and micro-animations
  - Dark mode support (planned)
  - Typography: a modern sans-serif (to be finalised)
- **Do not deviate from the Stitch design** without explicit approval
- All UI components should be built as reusable Flutter widgets
- Theme tokens (colours, typography, spacing, radii) should live in a single `lib/core/theme/` directory

---

## 15. Out of Scope (for now)

- Web/desktop deployment
- Payments or marketplace
- Video/audio calls
- AI-generated content features
- Integration with external social platforms

---

*Last updated: 2026-08-11*
