# Changelog

## 0.1.0-beta - 2026-09-21

Version code 16. The first beta. The alpha versions end here.

- **Updates: Ink Update.** Rebind has no internet permission, so it cannot
  look for a new version. Ink Update, an open source app of its own, does
  that: F-Droid first, then Google Play (it leaves an app that Google Play
  installed to Google Play), then GitHub. It makes a notification and opens
  the page. Setup has an "Updates" row that installs or opens it. The build
  for direct install carries it.
- The build for direct install carries Ink Dim too. Hardware hacks lists it.
- The lists of carried apps are named "Extensions".

- **Settings are safe across versions and across an uninstall.** An update
  always kept the settings: they are in the data of the app. An uninstall
  removed them. Now Android asks at uninstall whether to keep the data
  (`hasFragileUserData`), and Rebind keeps an automatic copy of the settings in
  `Documents/Rebind/rebind-settings.json`, which an uninstall does not touch.
  Import opens that folder. `StoredFormatTest` holds the texts that every
  0.0.x version stored, so a new version cannot stop reading them unseen.

## 0.0.15-alpha - 2026-09-21

Version code 15.

- **The Recents button opens Ink Recents.** Android does not let an app take
  the place of the recent-apps screen of the system. Rebind now sees that
  screen open (the task manager of the Viwoods launcher, or the stock Android
  one), closes it, and opens Ink Recents. It works for the Recents button of
  the bar, for the swipe, and for the Recents action. Home and recents has the
  switch "Recents button opens Ink Recents". It is on when Ink Recents is
  installed. Tests: `SystemRecentsTest`.

## 0.0.14-alpha - 2026-09-21

Version code 14.

- **Permissions covers the extensions again.** New items, each only where it
  can apply: "Install apps from Rebind" (the build that carries apps), "Ink
  Recents: app usage data" (when Ink Recents is installed), and "Home screen"
  to choose inkOS or ThinkLauncher (when one is installed). "Set up what is
  missing" walks through them too. The main screen still counts only the
  grants of Rebind itself.
- **Fix: voice typing said "The microphone is not allowed" although it was
  allowed.** Android gives the microphone to an app only while that app is in
  use. The Viwoods firmware does not count a speech app as in use while it
  listens in the background for another app, so Whisper was refused (error
  9). Rebind now goes to the speech screen of the speech app, where that app
  is in use, takes the words from its result, and remembers the route.
  Regression test: `DictationRouteTest`.
- **Fix: "Let Rebind get the Power hold" opened nothing.** Android has no
  request dialog for the assistant role. The row now opens the settings page
  "Default digital assistant app".

## 0.0.13-alpha - 2026-09-21

Version code 13.

- **Home screens: inkOS and ThinkLauncher in place of CLauncher.** The build
  for direct install carries inkOS v0.6 and ThinkLauncher v3.0, both made for
  e-ink, both GPL-3.0, each the release file of its maker and not changed.
  ThinkLauncher has the internet permission of its own. Rebind still has
  none.

- **Change a button from the Done step.** "Change what it does" and "Change
  how you press it" go back to those steps with the button kept. Back on the
  Done step goes to the actions too. Tests: `Route.back`.
- **Show or hide the button bar** is an action (build for direct install).
  Android 16 has no auto-hide for the three-button bar, so a button does it.
  It uses the shell commands of the Navigation screen and keeps the gestures
  as they are. The allow step asks for shell access for this action and for
  the light actions.
- **AI voice prompt** is an action of its own (Viwoods). It is what the
  firmware does on a hold of the AI key: the Viwoods AI screen, told to start
  its voice prompt. It needs the Viwoods AI account, as the stock hold does.
  A component launch can now carry text extras (`pkg/class?key=value`).
  Tests: `ComponentPayloadTest`.
- **Ask when the user tries it.** The first run asks for every grant once.
  After that the app asks at the moment something is missing: after a menu is
  saved, after the Power switch on the Navigation screen, when a Power press
  arrives while button remapping is off, and when voice typing starts with no
  microphone grant. Before, those places showed a short message or nothing.
- **Fix: system Back always closed the button setup.** From Android 13 the
  system does not call `onBackPressed` for an app with this target version.
  The setup now registers the Back callback, and Back goes one step back.
  Checked on the reader: Done, actions, how to press, main screen.

## 0.0.12-alpha - 2026-09-21

Version code 12.

- **Apps of other makers.** The build for direct install carries two apps and
  can install them: CLauncher v5.3.0 (the release APK of its maker, not
  changed) and Ink Recents 0.1.1 (open source). Home and recents lists them. Android asks before
  each install. The APKs are in the build, because Rebind has no internet
  permission. The Google Play build carries nothing and has no install
  permission: Google Play does not allow that here. It opens the page of the
  maker.
- Whisper 3.7 (speech to text on the device, MIT, the F-Droid build) is the
  third app that the build for direct install carries. Voice typing lists it.
- **The home screen of Rebind is gone**, with its settings screens. CLauncher
  is the home screen now, as its maker released it. An old settings file that
  has home screen settings still imports. Those settings are skipped.
- **Recent apps is a program of its own: Ink Recents** (open source,
  github.com/equwal/ink-recents). Rebind no longer has that screen, and no
  longer asks for usage access or `KILL_BACKGROUND_PROCESSES`. The Recent apps
  action opens Ink Recents. Old bindings keep working. Where Ink Recents is
  not installed, the action opens the screen that offers it.
- Hardware hacks: the double tap of Power is one row. Its way in is the camera
  intent or the wallet intent, as the device decides. There is no wallet
  button.
- The setup of a Power combination no longer says the same thing twice.

- **Hardware hacks** is a tile on the main screen with a screen of its own:
  hold Power (assistant role), double tap Power (camera intent), the wallet
  button, the full Power button (shell access), extra-dim light, and the
  button settings of the device. Advanced no longer holds them.

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
