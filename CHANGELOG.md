# Changelog

All notable changes to the Concierge iOS SDK. Versions follow semantic versioning.

## 0.1.2

- Fix: an offer card that resolves to a paywall closes the chat before it reaches `onOfferCard`, so a paywall the app opens from that handler is no longer presented under the chat sheet. The default handling (no `onOfferCard`) now also closes an embedded chat (`closeChat`) before calling `onPaywallCard`. Store offers keep the chat open: the purchase sheet shows over it.
- Docs: the `onOfferCard` samples close the chat with `Concierge.dismiss()` and show an error when a purchase fails, instead of leaving the customer in the chat with nothing shown.

## 0.1.1

- Card buttons are never dead. A review card whose store link is missing or does not open (no App Store app, such as the simulator) shows the system rating prompt (`AppStore.requestReview`) instead.
- Paywall cards close the chat before calling `onPaywallCard`, so the app's paywall is not stuck behind the chat sheet. Offers that resolve to a paywall do the same.
- With no `onPaywallCard` handler, a paywall card tap closes the chat, logs "Set Concierge.onPaywallCard to open your paywall" (also listed in the debug overlay) and emits the new `ConciergeEvent.paywallUnhandled(paywallId:)`.
- Device requests send `X-Concierge-Handlers` (`offer`, `paywall`, `offer,paywall` or `none`) so the dashboard can show whether cards are wired.
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
