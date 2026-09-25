# <p align="center">![icon_transparent.png](OpenParsec/Assets.xcassets/IconTransparent.imageset/icon_transparent.png) ![OpenParsec](OpenParsec/Assets.xcassets/LogoShadow.imageset/logo_shadow.png)</p>

## Korean keyboard edition

This repository contains a community build of [hugeBlack/OpenParsec](https://github.com/hugeBlack/OpenParsec)
for Korean Bluetooth keyboards connected to an iPad and a Windows host.

- Switch the Windows Korean IME with 한/영, Right Alt, Ctrl+Space, or Shift+Space.
- Release language-shortcut modifiers immediately so delayed Bluetooth key-up
  events do not leave Ctrl held while typing.
- Optionally tap Caps Lock for Esc, or hold Caps Lock with 1–9, 0, minus, or equals
  for F1–F12. Enable **Settings > Interactivity > Caps Lock as Esc / Fn**, then reconnect.

**[Download the keyboard edition IPA](https://github.com/zeberity123/OpenParsec/releases/tag/keyboard-2026-09-25)**
and install it with AltStore Classic. See [setup, settings, and device checks](KEYBOARD-BUILD.md).
Windows Korean Keyboard is enabled by default in this edition; disable it for
normal Right Alt/AltGr behavior. The Caps Lock mapping is off by default.

The downloads below are the original project's upstream builds and do not include
this edition's keyboard changes.

OpenParsec is a simple, open-source Parsec client for iOS/iPadOS written in Swift using the SwiftUI framework and the Parsec SDK.

This project is still a major WIP, so apologies for the currently lackluster documentation. I'm also very new to both Swift and SwiftUI so I'm sure there are many places for improvement.

Before building, make sure you have the Parsec SDK framework symlinked or copied to the `Frameworks` folder. Builds were tested on Xcode Version 12.5.

## Downloads
<a href="https://stikstore.app/altdirect/?url=https://github.com/hugeBlack/OpenParsec/releases/download/nightly/altstore.json" target="_blank">
   <img src="https://raw.githubusercontent.com/StikStore/altdirect/refs/heads/main/assets/png/AltSource_Blue.png" alt="Add AltSource" width="200">
</a>
<a href="https://github.com/hugeBlack/OpenParsec/releases/download/nightly/OpenParsec.ipa" target="_blank">
   <img src="https://raw.githubusercontent.com/StikStore/altdirect/refs/heads/main/assets/png/Download_Blue.png" alt="Download .ipa" width="200">
</a>

## Touch Control
You can set the touch mode you want to use in settings. Touchpad mode and direct touch mode are supported.

When streaming, you can tap with 3 fingers to bring up the on-screen keyboard.

You can toggle if you want to use 2 fingers to scroll or zoom in the overlay menu.

## Mouse & keyboard
USB mouse & keyboard are supported. 

## Game Controllers
When streaming, press any trigger button in your controller and parsec will recognize it. Make sure to configure the host properly (install virtual USB driver etc.) before using game controllers.

## Lag / Low Bitrate Issue
If you encounter lags from nowhere or your bitrate hardly goes over 10 Mbps, download Steam Link and do a network test. If you see constant lag spike in the graph, then it's a problem with Apple and there's little we can do to solve this problem. See [here](https://github.com/moonlight-stream/moonlight-ios/issues/627) for more disscussion. 

If you can't change your wireless router's channel to 149 like me, my personal experience is that you can try to power off the device you are using to stream as well as any nearby Apple devices, especially Mac, then only power on the device you are using to stream and do the aforementioned network test again. You can turn on other devices if the lag spike is gone and it may sustain for couple hours or days.
