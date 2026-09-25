# Personal Korean keyboard build

Target setup: iPad Pro 11-inch (3rd generation), iPadOS 18.7.8, LTBK21 Bluetooth
keyboard, Windows 11 with Microsoft Korean IME. Hardware verification is required;
the automated tests cannot reproduce iPadOS interception or Windows IME behavior.

## Keyboard behavior

`Settings > Interactivity > Windows Korean Keyboard` is enabled by default in this
personal build. It uses GameController physical keyboard events while streaming
and suppresses duplicate UIKit press forwarding. UIKit is the fallback when no
GameController keyboard is available. The original input path is available by
turning this setting off and reconnecting.

- Right Alt and the dedicated Hangul/LANG1 key send one Right Alt tap to Windows.
- Shift+Space and Ctrl+Space also send a Right Alt tap when delivered to the app.
  Hardware language shortcuts now release their accompanying modifiers immediately,
  with no timer or intentional delay. The modifiers stay released until physical
  key-up, so a keyboard's delayed Ctrl release cannot turn following letters into
  Ctrl shortcuts. Release and re-press Ctrl/Shift to use a new shortcut after switching.
  iPadOS may still reserve a system shortcut; use Right Alt or the touch button
  if a shortcut switches the iPad's own input source instead.
- The on-screen **한/영** button sends the same tap without a hardware shortcut.
- Keep Windows on **Korean Microsoft IME**, with **Korean keyboard (101-key) Type 1**.
  The remote IME performs composition; use an English hardware input source on
  the iPad while testing if local Korean composition interferes.
- `Backtick (~) as 한/영` is off by default. Enable it only if the LTBK21 still
  sends backtick for its language key. It also repurposes the real backtick key.
- Korean mode takes precedence over `Option Key as Command`. Other shortcuts
  keep their physical modifier keys. Turn Korean mode off for normal Right Alt
  combinations (such as AltGr).

### Esc and F1–F12 on compact keyboards

Enable **Settings > Interactivity > Caps Lock as Esc / Fn** (under Windows Korean
Keyboard), then reconnect. This optional mapping is off by default and applies
only while streaming with Windows Korean Keyboard enabled:

| Physical keys | Windows receives |
| --- | --- |
| Tap Caps Lock | Esc, on release |
| Hold Caps Lock + 1–9 | F1–F9 |
| Hold Caps Lock + 0 | F10 |
| Hold Caps Lock + minus | F11 |
| Hold Caps Lock + equals | F12 |

Hold Caps Lock before the number key. Shift/Ctrl/Alt can be added normally:
Shift+Caps Lock+5 sends Shift+F5. Releasing Caps Lock before the number key is
supported. Normal Caps Lock is replaced when enabled. If iPadOS changes language
instead, disable **Caps Lock to Switch to and from Latin** in iPad Settings >
General > Keyboard > Hardware Keyboard, if that option is shown. Leave Caps Lock
assigned to itself in iPadOS Modifier Keys for this app's layer to receive it.

The exact LTBK21 firmware shortcuts could not be verified from a manufacturer
manual. Try Fn with the printed Esc/F1–F12 keys first; this is a diagnostic trial,
not a confirmed LTBK21 combination. iPadOS shortcuts/media actions that never
reach OpenParsec cannot be remapped by the app. The Caps layer uses ordinary keys
instead and does not depend on receiving the keyboard's Fn key.

The upstream translator emits HID 144 for Hangul, but the bundled SDK's
`ParsecKeycode` does not define LANG1/Hangul. Right Alt (230) is supported. This
build translates the language keys explicitly rather than relying on that
undefined SDK mapping. This is a candidate fix, not proof of the exact cause of
the LTBK21's reported tilde behavior.

## Build and privacy

Use a **private standalone repository** under `zeberity123`. A GitHub fork of a
public repository cannot be made private. Keep upstream history and GPL notices.
The workflow builds on a GitHub macOS runner, runs Swift keyboard event tests,
and uploads a private Actions artifact for 14 days. It does not publish releases
or an AltStore source. Private macOS jobs consume the account's Actions allowance.

The IPA is ad-hoc signed for packaging; AltStore supplies device signing. No Apple
credentials or signing certificates are needed in GitHub. The bundle identifier
is `com.zeberity123.OpenParsec.Korean`, separate from the upstream installation.

## Install with AltStore Classic

1. Install AltServer on Windows using the official guide:
   https://faq.altstore.io/altstore-classic/how-to-install-altstore-windows
2. Connect and trust the iPad. Install AltStore Classic from AltServer. Enter your
   Apple ID directly in AltServer, and enable Developer Mode on the iPad.
3. Download and extract the private Actions artifact. Transfer
   `OpenParsec-Korean.ipa` to the iPad's Files app.
4. In AltStore Classic, open **My Apps**, tap **+**, and choose that IPA while
   AltServer is reachable. This is AltStore Classic, not AltStore PAL.
5. For a free Apple account, refresh within seven days. AltStore counts toward
   the three active sideloaded apps limit, so make room if necessary.

## Device validation

In Windows Notepad, select Korean Microsoft IME. Click into the document:

1. Tap the on-screen 한/영 button. Confirm the taskbar indicator changes A ↔ 가.
2. Press the LTBK21 한/영 key once. Confirm one switch with no `~` inserted. Hold
   it for a second and confirm it does not repeatedly switch.
3. Test Shift+Space and Ctrl+Space separately. Check the Windows indicator, not
   the iPad input-source indicator. Release Space before the modifier, then try
   the reverse release order. Subsequent typing must not have stuck modifiers.
4. Type `rksk` in Korean mode (가나), then switch back and type English. Check
   ordinary Space, Backspace, Shift+letter, Ctrl+C/V, and the real backtick key.
5. Disconnect/reconnect Bluetooth, background/resume the app, and reconnect the
   stream while keys are held. Confirm no repeats or modifiers remain stuck.
6. Tap 한/영 and immediately type, without waiting for Ctrl to release. Also test
   both release orders for Ctrl+Space/Shift+Space, then re-press Ctrl for Ctrl+C/V.
7. Enable Caps Lock as Esc / Fn. Test a Caps tap for Esc, Caps+2 for rename (F2),
   Caps+5 for refresh (F5), and all twelve keys in a key-event viewer. Check
   Shift+Caps+5, both release orders, and disconnect while a function key is held.

If only the physical language key fails, report whether the touch button works
and whether enabling `Backtick (~) as 한/영` changes the result. If the touch
button also fails, verify the Windows keyboard type and selected IME first.
