# Tähtipolku – Product Spec

## Current State

Tähtipolku is a vanilla HTML/CSS/JS children's reward board app.

- The MVP works.
- Has onboarding.
- Parents create children.
- Parents choose roles/avatars.
- Parents define good deeds.
- Parents choose how many stars each deed gives.
- Parents define reward tiers, thresholds, icons, labels, and prize text.
- Children collect stars.
- Each child has a magical star tree.
- A magical forest story layer exists.
- Data is stored locally in browser storage.
- The app is currently a single-file MVP.

## Core Product Rule

Do not rebuild into a complex parenting platform. Keep it a simple, magical reward board.

## Goal

Make Tähtipolku production-ready for Apple App Store and Google Play.

The app must become:
- visually premium
- more story-rich
- clearer for new parents
- account-based
- usable across multiple devices
- privacy-conscious
- child-safe
- localized
- store-ready

## Hard Rules

Children must NOT have accounts. Only parents have accounts. Children are profiles inside a family reward board.

## Do Not Add

- AI coach
- social features
- public profiles
- child login
- ads
- analytics (for now)
- complicated dashboards
- teacher/therapist mode
- routine platform complexity
- unnecessary tracking
- unnecessary permissions

## Product Model

Parent creates account → parent creates or loads family board → children exist as profiles → parent defines deeds and rewards → child earns stars → board syncs across parent devices.

---

## Working Style With Claude (IMPORTANT)

**The user is not a developer. Claude explains everything step by step.**

When Claude gives an instruction, it must describe exactly how to do it. Example:

> Bad: "Create a Supabase project."
>
> Good: "Go to supabase.com. Click 'Start your project' in the top right. Sign in with GitHub. Click 'New project'. Name it 'tahtipolku'. Select region 'Europe (Frankfurt)'. Copy the database password to a safe place. Click 'Create new project'. Wait about 2 minutes."

Rules:
- Every click, every URL, every selection must be stated.
- Assume zero prior knowledge.
- One thing at a time.
- Wait for confirmation before moving on.
- Claude replies to the user in Finnish. Specs and code comments are in English.

---

## UI Localization

UI will be multilingual. Languages are defined later (see Section 8). Do not hardcode UI strings in Finnish only — prepare a STRINGS object from the start.

Finnish is the default. English comes first after Finnish. Swedish, German, French, Spanish come later.

Parent-created content is NEVER translated:
- child names
- custom deeds
- reward labels
- prize text

---

## Roadmap

### 1. Preserve current MVP

- Do not rewrite from scratch.
- Do not change core kids/deeds/rewards/star logic unless necessary.
- Keep all current customizability.
- Make small, reviewable changes.

### 2. Add parent account system

- Add account screen before onboarding/main app.
- Options:
  - Create account
  - Sign in
  - Continue on this device without account
- Email/password first. Magic link later.
- Show logged-in parent email in settings/footer.
- Add sign out.
- Local-only mode must still work.

### 3. Backend / sync

Recommended backend: **Supabase**.

- Parent accounts via Supabase Auth.
- Use Supabase anon key only.
- Never expose service role key.
- Enable Row Level Security.
- Simple family workspace model.

Data model concept:
- `families`: one family board container
- `family_members`: parent users linked to families
- `reward_boards`: app state as JSON initially

Do not over-normalize. Storing the reward board as JSON is acceptable for v1.

### 4. Multi-device sync

- Logged-in users load their family board from Supabase.
- Same parent account works on multiple devices.
- LocalStorage remains as offline cache.
- When logged in, cloud is source of truth.
- When offline, app still works locally.
- When online returns, sync changes.
- Sync status indicators:
  - Saved
  - Saving
  - Offline — saved on this device
  - Syncing
  - Sync failed
- Conflict strategy v1: latest `updated_at` wins.

### 5. Migration from local-only to account

If user has a local board and then creates an account:
- Ask whether to move this device's board to the account.
- Do not wipe local data automatically.
- Options:
  - Move this board to my account
  - Start with empty cloud board
  - Cancel

### 6. Replace old privacy copy

Remove/replace copy saying:
- "No account"
- "No cloud"

New positioning:
- Parent account keeps Tähtipolku safe and available on your devices.
- Children do not need accounts.
- No ads.
- No public profiles.
- No social feed.
- Only data needed to save and sync the family board is stored.

### 7. Clear parent-facing explanation

A new parent must understand the app in 10 seconds.

Add a section in onboarding and a shorter version in the main app:
- Tähtipolku is a digital reward board for children.
- Parents define children.
- Parents define good deeds.
- Parents choose how many stars each deed gives.
- Parents define rewards and star thresholds.
- Children collect stars by doing good deeds.
- The magical forest story makes it fun and motivating.
- Parent account keeps the board synced across devices.
- Children do not need accounts.
- No ads or public profiles.

Tone: warm, simple, trustworthy, Finnish first. Not medical. Not therapy-sounding. Not too long.

### 8. Localization structure

Add language support before final visual redesign.

Languages:
- Finnish (default)
- English (first)
- Later: Swedish, German, French, Spanish

Requirements:
- Simple vanilla JS localization system.
- Store selected language.
- Language selector in settings/account/onboarding.
- Move all UI text into a STRINGS object.
- Do not translate parent-created content.

### 9. Expand story layer

Strengthen the magical forest world without adding complexity.

Use:
- Hopeapilvi
- Taikametsä
- Tähtipuu
- Kuutontut
- Taikametsän Kuningatar
- stars born from good deeds in the real world

Add short story copy to:
- onboarding
- reward tier section
- child star tree section
- first star moment
- near-reward moment
- reward unlocked popup
- zero-star state

Keep copy short, warm, magical. Do not hardcode practical rewards — the parent defines them.

### 10. New visual direction

After account + localization + content structure: production visual polish.

Visual style: premium Nordic magical forest. Warm, calm, magical, polished, trustworthy. App Store screenshot quality. Not cheap cartoon. Not too loud. Not cluttered.

Improve:
- onboarding
- account screen
- parent explanation card
- story card
- reward tier cards
- deed cards
- child cards
- star tree
- modals
- buttons
- empty states
- reward popup
- mobile spacing
- iPad layout
- typography hierarchy
- accessibility and contrast

Keep animations gentle. Add reduced motion support.

### 11. Parent gate

Protect child from accessing parent areas accidentally.

Require parent gate for:
- settings
- reset all stars
- sign out
- import/restore backup
- destructive actions

Simple math question is enough for v1. No child account needed.

### 12. Backup / export

Even with cloud sync, add export/import backup:
- Export board as JSON.
- Import board from JSON.
- Validate imported data.
- Confirm before replacing.
- Useful for support and trust.

### 13. Service worker / PWA hardening

- Make updates reliable.
- Avoid users stuck on old cached `index.html`.
- Use cache versioning.
- Network-first for HTML/navigation.
- Cache-first for static assets.
- Clean old caches.
- Keep offline support.

### 14. Store-readiness

Prepare for iOS/Android packaging later:
- Capacitor or similar wrapper.
- Minimal permissions.
- App icon.
- Splash screen.
- Privacy policy.
- Terms.
- Data deletion / contact instructions.
- App Store screenshots.
- Google Play Data Safety.
- Apple review demo account.

### Privacy / store rules

- Parent account only.
- No child login.
- No ads.
- No social / public profiles.
- No unnecessary SDKs.
- Avoid collecting child birthday / photo / location.
- Store only what is needed to operate and sync the reward board.

---

## Development Style

- Small commits.
- No "big rewrite".
- After each step, explain:
  - what changed
  - what files changed
  - how to manually test
  - what risks remain

## Immediate Next Step

Account preparation only:
- Add parent account screen.
- Add Supabase auth placeholders.
- Keep local-only mode working.
- Do not add sync yet.
