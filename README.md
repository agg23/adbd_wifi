# adbd_wifi

Custom adbd staticly linked build (taken from AOSP source) with functionality stripped so that it can run in userland and provide TCP ADB access. Designed for very locked down Android devices like the [Humane Ai Pin](https://github.com/openaipin).

## Usage

Connect the device over USB (or any other available transport). Run:

```bash
adb push adbd_wifi /data/local/tmp/adbd_wifi
adb shell chmod +x /data/local/tmp/adbd_wifi

# Start process in the background
adb shell "nohup sh -c \"./data/local/tmp/adbd_wifi &\""
```

You can terminate the last `adb shell` command and `adbd_wifi` will remain running. You should now be able to access the device over the network via `adb connect [ip]`.

## Functionality

* `shell`
* scrcpy

## Known issues

* Does not require authentication
* JDWP probably doesn't work
* APK install via Android Studio seems to not work, but `adb install -r` does

## FAQ

### Why Android 10?

I wanted this project to be built entirely on GitHub hosted workers. Due to the large dependency tree of the AOSP codebase, Android 10 was the latest that I managed to get to fit on the runner (ended up taking ~69GB).
