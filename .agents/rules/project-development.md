# Stitch — AI Agent Development Rules

These rules apply to **every AI agent** (Antigravity, Copilot, Gemini, GPT, Claude, or any other) that works on this project.
Violating these rules risks breaking a working app or diverging from the agreed product design.

---

## Mandatory Reading Before Starting Any Session

Before making **any architectural, structural, or feature decision**, you MUST read the following files in order:

1. **`PROJECT_CONTEXT.md`** — product vision, agreed feature set, navigation structure, Wonder Chat rules, community system, Firebase architecture, and design direction. If you haven't read this, stop and read it now.
2. **`TODO.md`** — the phased development roadmap. Check which phase is current and which tasks are pending vs. done.
3. **`DEVELOPMENT_LOG.md`** — the history of what has been built, tested, and verified. Never assume something exists; check the log.

---

## Code Inspection Before Modification

- **Always inspect existing code** before modifying it. Use `view_file` or `list_dir` to understand what is already there.
- **Never assume** the state of any file. Always read it first.
- **Never unnecessarily rewrite working code.** If a widget, function, or file already works correctly, leave it alone unless the task explicitly requires changing it.
- When extending a feature, prefer **adding** new files/widgets over **rewriting** existing ones.

---

## Keeping Files Up to Date

After completing any significant task:

- **Update `TODO.md`** — mark completed items as `[x]`, in-progress as `[~]`, and update the "Last updated" date.
- **Update `DEVELOPMENT_LOG.md`** — add a new session entry describing what was done, the current state of the codebase, and what comes next.

After a **major session** (multiple features or architectural changes), always update both files before ending the session.

---

## Cross-Platform Compatibility

- This is a **Flutter app targeting Android and iOS**. Every change must work on both platforms.
- Never add Android-only or iOS-only workarounds without clearly marking them and confirming with the developer.
- Always check that new packages support both `android` and `ios` in their `pubspec.yaml` / pub.dev page.
- Run or recommend running `flutter analyze` on both platform targets after significant changes.

---

## Visual Design — Stitch Design System

- Follow the **Stitch visual design** at all times. Do not invent new colour schemes, font families, or layout patterns.
- All theme tokens (colours, typography, spacing, border radii) must come from `lib/core/theme/`. Do not hardcode design values inline.
- Build UI as **reusable, composable Flutter widgets** in `lib/shared/widgets/` or the relevant feature folder.
- Do not introduce Material Design's default purple/blue colour scheme — the Stitch palette overrides it.
- Dark mode must be considered when adding any UI component (use theme-aware colours, not hardcoded hex values).

---

## Security Rules — Non-Negotiable

- **NEVER commit secrets.** API keys, Firebase service account files, tokens, and passwords must never be hardcoded in Dart files or committed to Git.
  - Use `.env` files (excluded from Git via `.gitignore`) or environment variables.
  - Firebase config files (`google-services.json`, `GoogleService-Info.plist`) are exceptions IF they contain only public client config (no service account keys).
- **NEVER make production or backend changes** (Firestore Security Rules, Cloud Functions, Firebase project settings) without explicit developer approval.
- **NEVER bypass authentication** in code, even for testing. Use Firebase Auth emulator for local testing.
- **NEVER write Firestore Security Rules that are open/permissive** (e.g., `allow read, write: if true`). All rules must enforce authentication and authorisation.

---

## Change Philosophy — Small, Safe, and Testable

- **Prefer small, targeted changes** over large refactors.
  - If a task feels like it requires rewriting half the codebase, stop and discuss it with the developer first.
- **One logical concern per change.** Don't mix UI changes, data model changes, and routing changes in a single session without documenting each step.
- **Test after every meaningful change:**
  - Run `flutter analyze` — zero errors required.
  - Run `flutter test` — all tests must pass.
  - If you add new functionality, add a corresponding unit or widget test.
- **Never introduce breaking changes** to existing working features without explicit approval.

---

## Firebase — Do Not Integrate Without Approval

- Firebase has **not yet been added** to this project. Do not add any Firebase packages, run `flutterfire configure`, or add `google-services.json` / `GoogleService-Info.plist` unless the developer has explicitly instructed you to begin Phase 2.
- When Firebase integration is approved, follow the FlutterFire CLI setup process and document every step in `DEVELOPMENT_LOG.md`.

---

## Package Management

- Do not add packages to `pubspec.yaml` without a clear, approved reason.
- For every new package, verify:
  - It supports Android and iOS
  - It has active maintenance (recent pub.dev activity)
  - It does not introduce unnecessary permissions on either platform
- Prefer packages from the official FlutterFire suite for Firebase-related functionality.
- Do not add packages just for convenience if the same result can be achieved with Flutter's built-in tools.

---

## Summary Checklist (run through this at the start of every session)

- [ ] Have I read `PROJECT_CONTEXT.md`?
- [ ] Have I read `TODO.md` and identified the current phase?
- [ ] Have I read `DEVELOPMENT_LOG.md` to understand the current state?
- [ ] Have I inspected the existing code before making changes?
- [ ] Is this change Android AND iOS compatible?
- [ ] Does this change follow the Stitch design system?
- [ ] Have I avoided hardcoding secrets?
- [ ] Is this a small, testable change?
- [ ] Have I run (or will I run) `flutter analyze` and `flutter test`?
- [ ] Will I update `TODO.md` and `DEVELOPMENT_LOG.md` when done?
