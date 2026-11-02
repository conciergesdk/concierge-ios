# Concierge for iOS

In-app support chat for iOS apps. Native SwiftUI, zero dependencies, iOS 16+ and Mac Catalyst 16+.

This repository hosts the Swift package for the prebuilt `Concierge.xcframework`. The SDK is
distributed as a binary; this repository contains no SDK source code.

## Install

Swift Package Manager. In Xcode: File > Add Package Dependencies, enter
`https://github.com/conciergesdk/concierge-ios`, choose "Up to Next Major" and add the
`Concierge` product to your app target.

In `Package.swift`:

```swift
.package(url: "https://github.com/conciergesdk/concierge-ios.git", from: "0.1.1")
// target dependency
.product(name: "Concierge", package: "concierge-ios")
```

Or let the CLI do it: `npx @conciergesdk/cli init`.

## Quick start

```swift
import Concierge
import SwiftUI

@main
struct MyApp: App {
    init() {
        Concierge.configure(appKey: "app_YOUR_APP_KEY")
    }

    var body: some Scene {
        WindowGroup {
            ContentView()
                .conciergeSupportButton()
        }
    }
}
```

Or open the chat from your own control: `Button("Contact Support") { Concierge.present() }`.

Full guide: https://conciergesdk.com/docs/ios

## What is in the binary

- `Concierge.xcframework`: iOS device (arm64), iOS Simulator (arm64, x86_64) and Mac Catalyst slices.
- Built with library evolution, so it works with this and later Xcode and Swift versions.
- Strings in 34 languages (`Localizable.strings`) and a privacy manifest (`PrivacyInfo.xcprivacy`) that
  Xcode merges into your app's privacy report.

## Privacy

The SDK sends the messages, photos and identity you pass it (user ID, name, email), device details
and errors to your Concierge workspace to provide support. It does not track users and contains
no third-party SDKs. See `PrivacyInfo.xcprivacy` inside the framework.

## License

Free to use with a Concierge account. See [LICENSE](LICENSE).
