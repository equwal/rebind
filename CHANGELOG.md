# Changelog

## 0.0.11-alpha - 2026-09-21

Version code 11.

- **Fix: a Camera key in the drawing of a device that has none.** The Viwoods
  reader declares a camera key to Android and has no such button. Detection
  put the declared key in the drawing. The drawing now shows only the buttons
  that the device profile knows, and a button that was really pressed in
  normal use. The Detect screen still lists what the device declares, and
  marks a key that was never seen. Regression test: `DeviceKeysTest`.
  The double tap of Power uses the camera *intent* of Android. It needs no
  camera button.

## 0.0.10-alpha - 2026-09-21

Version code 10.

- **No Google Play, no lock.** On a device where the Google Play app is not
  installed or is turned off, the app is free and complete. There is no way
  to buy there, so there is nothing to lock. The licence screen says "Free on
  this device". A bought licence still comes first. Tests: `LicenseDecideTest`.
- The build for direct install has a tip link on the Licence screen
  (ko-fi.com/truex). A tip unlocks nothing. The Google Play build has no such
  link, because Google Play does not allow it.
- The reasons in the allow step are hints of three to seven words. The app
  says "double tap" for Power too.

## 0.0.9-alpha - 2026-09-21

Version code 9.

- **New name: Rebind.** The name says what the app does, and it has the words
  that buyers type in Play search. The package id stays `dev.equwal.assistkey`,
  so an update keeps all settings. The settings file keeps its `AssistKey`
  marker, so old exports still import.
- **Recent apps.** Swipe up closes the app. Swipe down closes all the others.
  One swipe sideways moves one card in one step, with no glide. When the screen
  opens, the card jumps up and sideways once to show the swipes. "Close all but
  this app" and "Close all" are two tall buttons with space between them.
  Closing works without shell access too: Android ends the background
  processes of the app (`KILL_BACKGROUND_PROCESSES`, a normal permission).
- **Hardware hacks** have their own box under Advanced: hold Power, double
  press Power, the wallet button, the full Power button, extra-dim light, and
  the button settings of the device.
- **Ask when it is needed, everywhere.** A binding made under Advanced now opens
  the same "allow" step as the guided setup, when something is missing.
- **The drawing is the main screen.** The device and its buttons are on the
  first screen. Each button shows what it does now. Tap a button to set it up.
  Tap two buttons to set up a combination.
- **Button order.** A device profile gives the order of its buttons from the
  top down. Viwoods AiPaper: Power, Volume up, Volume down, AI key.
- **On-screen button.** A new button that needs no hardware: a small round
  button that floats over every app. Tap it to do the action, drag it to move
  it. The key filter draws it, only while it has an action. Android's own
  accessibility button is not used, because Android shows that button to every
  user as soon as a service asks for it.
- **More ways to press.** Step two lists tap, double tap, triple tap, hold, 4
  taps and 5 taps, and an Advanced row with every gesture of the button.
- **More actions.** Step three adds Lock screen and Screenshot, and an Advanced
  row with every action.
- **Ask when it is needed.** A Power press that Android hides from apps is now
  offered where the build can have shell access. The app then asks for shell
  access, which opens the full Power button. After a double press of Power is
  set up, the app offers the wallet way for devices that use it.
- **Device detection.** At first start the app finds which buttons the device
  has, and what the device can do. It never asks the user to press a button.
  Advanced > Detect this device shows the result. The device report has it too.
- **Less text.** All "More about this" rows are gone. Notes are one short
  sentence. The accessibility disclosure is short. Google Play requires it, so
  it stays.
- Tests: selection rules of the drawing, the on-screen button route, shell
  access as a need, detection parser and round trip.
