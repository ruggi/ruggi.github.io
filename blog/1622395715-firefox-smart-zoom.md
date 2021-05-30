# Double-tap zoom on Firefox

Firefox now supports the double-tap "smart zoom" feature, similar to the one of Safari, on macOS.

Unless I'm mistaken, this has been enabled with [this commit](https://github.com/mozilla/gecko-dev/commit/7d1fc308716c5ff5d2c3ec04b7c3bb4432d6060d). Weirdly there are two different settings to have the feature fully enabled, but still, it works pretty well - not as polished as on Safari, but it gets the job done.

To enable it, head to `about:config` and make sure these two settings are set to `true`:

* `apz.allow_double_tap_zooming`
* **`apz.mac.enable_double_tap_zoom_touchpad_gesture`**

Yay!
