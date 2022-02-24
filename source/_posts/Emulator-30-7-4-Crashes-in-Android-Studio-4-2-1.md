---
title: Emulator 30.7.4 Crashes in Android Studio 4.2.1
date: 2021-06-24 14:03:05
tags:
---
All emulators in AVD failed to run after I *accidentally* update Android Studio to 4.2.1 on macOS Catalina (10.15.7).

You can find more debug details if you run the emulator in terminal.
```bash
emulator -list-avds
emulator -avd your_avd_name
```

## Solution

Downgrade (sort of) amulator to 30.4.5 (build_id 7140946)
https://dl.google.com/android/repository/emulator-darwin_x64-7140946.zip

First, downlaod the zip file and unzip it.
Then, find the emulator folder under sdk folder. Replace the items inside with what you have downloaded.
Restart Android Studio (for example, go to menu File, select Invalidate Caches / Restart) and try to run the emulators again.

You will see the warnings saying something, like, these files can not be verified due to unknown developer. Remember to go to Mac System Preference, Security & Privacy, under the General tab, allow these apps to run. Eventually, everything will be fine. Good luck.


Ref:
https://issuetracker.google.com/issues/191799887
https://issuetracker.google.com/issues/191805460
https://medium.com/nerd-for-tech/how-to-downgrade-android-emulator-on-macos-6e611d2d2bcb