# Quad-speaker (4-channel) audio — Galaxy Tab A7 (gta4l / gta4lwifi)

Technical note for maintainers. The Tab A7 (SM-T505 / SM-T500) has **four speakers**;
Samsung's stock ROM drives all four. On a plain AOSP/LineageOS port the framework often
negotiates only **stereo** to the speaker, so two of the four stay quiet or duplicate.

## The fix

The ROM-side enabler is the **speaker output `channelMasks`** in the audio policy. The
default speaker `devicePort` advertises up to `AUDIO_CHANNEL_OUT_STEREO`; extend it so the
audio framework can negotiate multichannel (incl. **QUAD**) output to the speaker sink.

**File:** `device/samsung/gta4l-common/audio/configs/audio_policy_configuration.xml`

For every mix port that feeds the speaker **and** the `Speaker` `devicePort`
(`type="AUDIO_DEVICE_OUT_SPEAKER"`), the `channelMasks` list includes:

```
channelMasks="AUDIO_CHANNEL_OUT_MONO,AUDIO_CHANNEL_OUT_STEREO,AUDIO_CHANNEL_OUT_2POINT1,\
AUDIO_CHANNEL_OUT_QUAD,AUDIO_CHANNEL_OUT_PENTA,AUDIO_CHANNEL_OUT_5POINT1,\
AUDIO_CHANNEL_OUT_6POINT1,AUDIO_CHANNEL_OUT_7POINT1"
```

The important one is **`AUDIO_CHANNEL_OUT_QUAD`** (mask `0x33`). With it advertised, the
framework/AudioFlinger will hand a 4-channel stream to the vendor audio HAL, which routes
the channels to the four speaker amps via the stock Qualcomm/Samsung paths.

You can confirm it took at runtime:

```
adb shell dumpsys media.audio_policy | grep -A2 Speaker      # QUAD (0x33) in the mask list
```

## What is NOT changed

- The **per-amp routing** (which channel → which physical speaker) is done by the stock
  vendor audio HAL + `mixer_paths_qrd.xml` / `audio_platform_info_qrd.xml` from the Samsung
  blobs — no custom mixer edit was needed on this device; the missing piece was purely the
  policy channel mask.
- No extra amp library or property is required.

## Files to look at (all open in the device tree)

- `audio/configs/audio_policy_configuration.xml` — **the change** (speaker channel masks).
- `audio/configs/mixer_paths_qrd.xml`, `audio_platform_info_qrd.xml`, `wt_cust_audio.xml` —
  stock Qualcomm/Samsung routing, referenced for completeness.

## Porting to another Samsung/QCOM tablet with multiple speakers

1. Find your `audio_policy_configuration.xml` (device tree or `/vendor/etc`).
2. Add `AUDIO_CHANNEL_OUT_QUAD` (and higher, if the HAL supports them) to the `channelMasks`
   of the mix ports feeding the speaker and of the `Speaker` `devicePort`.
3. Rebuild, then verify with `dumpsys media.audio_policy` and by ear.
   If channels still don't separate, the vendor HAL/`mixer_paths` may need the stock quad
   speaker path — pull it from the stock ROM.
