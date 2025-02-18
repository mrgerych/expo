---
title: Brightness
---

An API to get and set screen brightness.

On Android, there is a global system-wide brightness setting, and each app has its own brightness setting that can optionally override the global setting. It is possible to set either of these values with this API. On iOS, the system brightness setting cannot be changed programmatically; instead, any changes to the screen brightness will persist until the device is locked or powered off.

### Methods
- [`Expo.Brightness.getBrightnessAsync()`](#expobrightnessgetbrightnessasync)
- [`Expo.Brightness.setBrightnessAsync(brightnessValue)`](#expobrightnesssetbrightnessasyncbrightnessvalue)
- [`Expo.Brightness.useSystemBrightnessAsync()`](#expobrightnessusesystembrightnessasync)
- [`Expo.Brightness.isUsingSystemBrightnessAsync()`](#expobrightnessisusingsystembrightnessasync)
- [`Expo.Brightness.getSystemBrightnessAsync()`](#expobrightnessgetsystembrightnessasync)
- [`Expo.Brightness.setSystemBrightnessAsync(brightnessValue)`](#expobrightnesssetsystembrightnessasyncbrightnessvalue)
- [`Expo.Brightness.getSystemBrightnessModeAsync()`](#expobrightnessgetsystembrightnessmodeasync)
- [`Expo.Brightness.setSystemBrightnessModeAsync(brightnessMode)`](#expobrightnesssetsystembrightnessmodeasyncbrightnessmode)

### Enum Types
- [`Expo.Brightness.BrightnessMode`](#expobrightnessbrightnessmode)

### Errors
- [Error Codes](#error-codes)

## Methods

### `Expo.Brightness.getBrightnessAsync()`

Gets the current brightness level of the device's main screen.

#### Returns

A `Promise` that is resolved with a number between 0 and 1, inclusive, representing the current screen brightness.

---

### `Expo.Brightness.setBrightnessAsync(brightnessValue)`

Sets the current screen brightness. On iOS, this setting will persist until the device is locked, after which the screen brightness will revert to the user's default setting. On Android, this setting only applies to the current activity; it will override the system brightness value whenever your app is in the foreground.

#### Arguments

- **brightnessValue (_number_)** - A number between 0 and 1, inclusive, representing the desired screen brightness.

#### Returns

A `Promise` that is resolved when the brightness has been successfully set.

#### Error Codes

- `ERR_BRIGHTNESS` - An unexpected OS error occurred when trying to set the brightness. See the `nativeError` object for more information.

---

### `Expo.Brightness.useSystemBrightnessAsync()`

**Android only.** Resets the brightness setting of the current activity to use the system-wide brightness value rather than overriding it.

#### Returns

A `Promise` that is resolved when the setting has been successfully changed.

---

### `Expo.Brightness.isUsingSystemBrightnessAsync()`

**Android only.** Returns a boolean specifying whether or not the current activity is using the system-wide brightness value.

#### Returns

A `Promise` that resolves with `true` when the current activity is using the system-wide brightness value, and `false` otherwise.

#### Error Codes

- `ERR_BRIGHTNESS` - An unexpected OS error occurred when trying to set the brightness. See the `nativeError` object for more information.

---

### `Expo.Brightness.getSystemBrightnessAsync()`

**Android only.** Gets the global system screen brightness.

#### Returns

A `Promise` that is resolved with a number between 0 and 1, inclusive, representing the current system screen brightness.

#### Error Codes

- `ERR_BRIGHTNESS_SYSTEM` - An unexpected OS error occurred when trying to get the system brightness. See the `nativeError` object for more information.

---

### `Expo.Brightness.setSystemBrightnessAsync(brightnessValue)`

> **WARNING:** This method is experimental.

**Android only.** Sets the global system screen brightness and changes the brightness mode to `MANUAL`. Requires `SYSTEM_BRIGHTNESS` permissions.

#### Arguments

- **brightnessValue (_number_)** - A number between 0 and 1, inclusive, representing the desired screen brightness.

#### Returns

A `Promise` that is resolved when the brightness has been successfully set.

#### Error Codes

- `ERR_BRIGHTNESS_PERMISSIONS_DENIED` - The user did not grant `SYSTEM_BRIGHTNESS` permissions.
- `ERR_BRIGHTNESS_SYSTEM` - An unexpected OS error occurred when trying to set the system brightness. See the `nativeError` object for more information.

#### Example

```javascript
await Permissions.askAsync(Permissions.SYSTEM_BRIGHTNESS);

const { status } = await Permissions.getAsync(Permissions.SYSTEM_BRIGHTNESS);
if (status === 'granted') {
  Expo.Brightness.setSystemBrightnessAsync(1);
}
```

---

### `Expo.Brightness.getSystemBrightnessModeAsync()`

**Android only.** Gets the system brightness mode (e.g. whether or not the OS will automatically adjust the screen brightness depending on ambient light).

#### Returns

A `Promise` that is resolved with a [`BrightnessMode`](#expobrightnessbrightnessmode). Requires `SYSTEM_BRIGHTNESS` permissions.

#### Error Codes

- `ERR_BRIGHTNESS_MODE` - An unexpected OS error occurred when trying to get the brightness mode. See the `nativeError` object for more information.

---

### `Expo.Brightness.setSystemBrightnessModeAsync(brightnessMode)`

**Android only.** Sets the system brightness mode.

#### Arguments

- **brightnessMode (_[BrightnessMode](#expobrightnessbrightnessmode)_)** - One of `BrightnessMode.MANUAL` or `BrightnessMode.AUTOMATIC`. The system brightness mode cannot be set to `BrightnessMode.UNKNOWN`.

#### Returns

A `Promise` that is resolved when the brightness mode has been successfully set.

#### Error Codes

- `ERR_INVALID_ARGUMENT` - An invalid argument was passed. Only `BrightnessMode.MANUAL` or `BrightnessMode.AUTOMATIC` are allowed.
- `ERR_BRIGHTNESS_MODE` - An unexpected OS error occurred when trying to set the brightness mode. See the `nativeError` property of the thrown error for more information.
- `ERR_BRIGHTNESS_PERMISSIONS_DENIED` - The user did not grant `SYSTEM_BRIGHTNESS` permissions.

## Enum Types

### BrightnessMode

- **`BrightnessMode.AUTOMATIC`** - Mode in which the device OS will automatically adjust the screen brightness depending on the ambient light.
- **`BrightnessMode.MANUAL`** - Mode in which the screen brightness will remain constant and will not be adjusted by the OS.
- **`BrightnessMode.UNKNOWN`** - Means that the current brightness mode cannot be determined.

## Error Codes

| Code | Description |
| --- | --- |
| `ERR_BRIGHTNESS` | An error occurred when getting or setting the app brightness. |
| `ERR_BRIGHTNESS_MODE` | An error occurred when getting or setting the system brightness mode. |
| `ERR_BRIGHTNESS_PERMISSIONS_DENIED` | An attempt to set the system brightness was made without the proper permissions from the user. |
| `ERR_BRIGHTNESS_SYSTEM` | An error occurred when getting or setting the system brightness. |
