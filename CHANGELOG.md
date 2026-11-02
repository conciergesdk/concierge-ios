# Changelog

All notable changes to the Concierge iOS SDK. Versions follow semantic versioning.

## Unreleased

- `Concierge.maybeRequestReview(moment:)`: asks StoreKit for a rating only when local rules (install age, 3 per 365 days, 90 day cooldown, once per version, never over the chat) and the server (no recent complaint or negative sentiment) allow it. Returns `ReviewPromptResult` (`shown`, `reason`).
- `Concierge.reviewPromptAfterSupport` (default true): checks `.supportResolved` about a second after the chat closes.
- `ConciergeEvent.reviewPromptShown(moment:)`.
- While suspended, `maybeRequestReview` returns `suspended` without a request and the after support check never runs. `reset()` clears the review history.

## 0.1.0

First public release.

- In-app support chat in native SwiftUI: `Concierge.present()`, `ConciergeChatView`, `.conciergeSupportButton()`.
- History cached on the device, unlimited paging, offline outbox, live updates over a WebSocket.
- Photos, typing indicator, read receipts, review, paywall and offer cards with StoreKit 2 redemption.
- App context, errors and client tools the AI or the team can run with the user's consent.
- Shipped as a prebuilt `Concierge.xcframework` with library evolution, localizations and a privacy manifest.
