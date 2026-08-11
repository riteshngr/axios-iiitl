# Stitch — Development Roadmap (TODO)

> Update this file after completing any significant task.
> Mark items with [x] when done, [~] when in progress, and [ ] when pending.

---

## Phase 0 — Project Foundation ✅

- [x] Create Flutter project (`flutter create iiitl`)
- [x] Verify Android device debugging
- [x] Run default Flutter counter app on physical Android device
- [x] Initialise Git repository
- [x] Push repository to GitHub
- [x] Create `PROJECT_CONTEXT.md` (product vision & feature spec)
- [x] Create `TODO.md` (this file)
- [x] Create `DEVELOPMENT_LOG.md`
- [x] Create `.agents/rules/project-development.md` (AI agent rules)

---

## Phase 1 — Project Structure & Design System

- [ ] Establish folder architecture inside `lib/`
  - `lib/core/` — theme, constants, utilities, routing
  - `lib/features/` — one sub-folder per feature
  - `lib/shared/` — shared widgets and models
- [ ] Create `lib/core/theme/app_theme.dart` — colour palette, typography, spacing tokens
- [ ] Create `lib/core/theme/app_colors.dart` — brand colour constants
- [ ] Create `lib/core/theme/app_text_styles.dart` — text style definitions
- [ ] Set up app router (`go_router` or Navigator 2.0)
- [ ] Create stub screens for each bottom tab (Home, Community, Need, Profile)
- [ ] Create main scaffold with bottom navigation bar
- [ ] Stub Inbox screen (DMs + Wonder Chat sections)
- [ ] Update `lib/main.dart` to use the new app structure and theme
- [ ] Run `flutter analyze` — zero errors
- [ ] Run `flutter test` — all tests pass

---

## Phase 2 — Firebase Integration & Authentication

- [ ] Add Firebase to the Flutter project (FlutterFire CLI)
  - Android (`google-services.json`)
  - iOS (`GoogleService-Info.plist`)
- [ ] Add Firebase packages: `firebase_core`, `firebase_auth`, `cloud_firestore`, `firebase_storage`
- [ ] Implement Firebase Auth with institute email domain validation (`@iiitl.ac.in`)
- [ ] Create login screen (Stitch design)
- [ ] Create registration screen (Stitch design)
- [ ] Create email verification flow
- [ ] Create Firestore user document on first sign-in
- [ ] Implement auth state routing (unauthenticated → login, authenticated → home)
- [ ] Write Firestore Security Rules (users collection)
- [ ] Test auth on Android and iOS

---

## Phase 3 — Student Profile

- [ ] Design and implement Profile screen UI
- [ ] Fetch and display user data from Firestore
- [ ] Allow profile editing (display name, bio, year, branch, avatar)
- [ ] Implement avatar upload to Firebase Storage
- [ ] Display joined communities list on profile
- [ ] Display post / Need activity history (with privacy toggles)
- [ ] Show Wonder Chat connection count and open-to-chat status
- [ ] Write Firestore Security Rules (profile read/write)

---

## Phase 4 — Community System

- [ ] Design Community listing screen (browse / discover)
- [ ] Implement community data model in Firestore
- [ ] Community detail screen (banner, description, members, posts)
- [ ] Join / leave community functionality
- [ ] Create community request form (student-created communities)
- [ ] Admin approval queue for community requests
- [ ] Post creation within a community (text, image, link)
- [ ] Post detail screen
- [ ] Nested comment system (Reddit-style threading)
- [ ] Upvote / downvote on posts and comments
- [ ] Pinned posts (moderator action)
- [ ] Community roles (Member, Moderator, Admin)
- [ ] Official community verified badge
- [ ] Write Firestore Security Rules (communities, posts, comments)

---

## Phase 5 — Home Feed

- [ ] Implement aggregated home feed (communities + announcements + Needs)
- [ ] Feed card components for posts and Needs
- [ ] Announcement highlight / pinned section at top of feed
- [ ] Feed filtering by category
- [ ] Pagination / infinite scroll
- [ ] Pull-to-refresh

---

## Phase 6 — Need Feature

- [ ] Need data model in Firestore
- [ ] Need creation form (title, description, category, urgency, expiry, contact pref)
- [ ] Need listing screen with filter/search
- [ ] Need detail screen
- [ ] Respond to Need via comment or DM
- [ ] Auto-close Need on expiry date
- [ ] Mark Need as fulfilled
- [ ] Write Firestore Security Rules (needs collection)

---

## Phase 7 — Inbox: Direct Messages

- [ ] DM data model in Firestore
- [ ] Inbox screen with conversation list
- [ ] 1:1 DM conversation screen (real-time via Firestore listeners)
- [ ] Send / receive text messages
- [ ] Read receipts
- [ ] Notification badge on Inbox icon
- [ ] Write Firestore Security Rules (DM collections — strict: only participants)

---

## Phase 8 — Wonder Chat

- [ ] Wonder Chat data model in Firestore
- [ ] Wonder Chat matching logic (pairing algorithm — TBD)
- [ ] Wonder Chat conversation screen (slow-messaging UI)
- [ ] Message quality filter (server-side via Cloud Functions)
- [ ] Progress indicator — messages toward 100
- [ ] Connection unlock event when 100 messages reached
- [ ] Move unlocked Wonder Chat to DMs
- [ ] Active Wonder Chat limit enforcement
- [ ] Write Firestore Security Rules (wonderChats — strict privacy)

---

## Phase 9 — Announcements

- [ ] Announcement data model in Firestore
- [ ] Announcement creation (admin-only via secure path)
- [ ] Display announcements in Home feed (pinned/highlighted)
- [ ] Push notification for new announcements (FCM)
- [ ] Announcement detail screen

---

## Phase 10 — Moderation & Admin

- [ ] Reporting flow for posts, comments, profiles, communities
- [ ] Moderation queue in Firestore
- [ ] Community moderator actions (remove post/comment, ban from community)
- [ ] Master Admin panel (likely separate web app — future)
- [ ] Account suspension and ban logic
- [ ] Audit log for moderation actions

---

## Phase 11 — Polish & Production Readiness

- [ ] Dark mode implementation
- [ ] Accessibility audit (contrast, font sizes, screen reader)
- [ ] Performance profiling on Android and iOS
- [ ] Implement Firebase App Check
- [ ] Finalise Firestore Security Rules (all collections)
- [ ] Set up Firebase Analytics events
- [ ] Beta testing with real students
- [ ] App Store / Play Store submission preparation
- [ ] Review and finalise content moderation policy

---

## Ongoing

- [ ] Run `flutter analyze` after every significant change
- [ ] Run `flutter test` after every significant change
- [ ] Keep `DEVELOPMENT_LOG.md` up to date
- [ ] Never commit secrets or API keys to Git

---

*Last updated: 2026-08-11*
