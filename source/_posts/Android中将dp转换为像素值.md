---
title: Android中将dp转换为像素值
date: 2017-10-16 12:39:04
tags: [Android,适配]
categories: Android
---

# 如何在Android中将dp转换为像素值？

在某些情况下，您需要以 `dp` 表示尺寸，然后将它们转换为 像素。设想一个在用户 手指移动至少 16 像素之后可以识别滚动或滑动手势的应用。在基线屏幕上，用户必须移动 `16 pixels / 160 dpi`（等于一英寸的 1/10 或 2.5 毫米），然后才会识别该手势。在 具有高密度显示屏 (240dpi) 的设备上，用户必须移动 `16 pixels / 240 dpi`（等于 一英寸的 1/15 或 1.7 毫米）。此距离更短，应用因此 似乎对用户更灵敏。

```java
// The gesture threshold expressed in dp
private static final float GESTURE_THRESHOLD_DP = 16.0f;

// Get the screen's density scale
final float scale = getResources().getDisplayMetrics().density;
// Convert the dps to pixels, based on density scale
mGestureThreshold = (int) (GESTURE_THRESHOLD_DP * scale + 0.5f);

// Use mGestureThreshold as a distance in pixels...
```

[DisplayMetrics.density](https://developer.android.com/reference/android/util/DisplayMetrics.html#density)字段根据当前屏幕密度指定 将 `dp` 单位转换为像素必须使用的缩放系数。 在中密度屏幕上，[DisplayMetrics.density](https://developer.android.com/reference/android/util/DisplayMetrics.html#density)等于 1.0；在高密度屏幕上，它等于 1.5；在超高密度屏幕上，等于 2.0； 在低密度屏幕上，等于 0.75。此数字是一个系数，应用其乘以 `dp` 单位以获取用于当前屏幕的实际像素数。（然后在转换时加上 `0.5f`，将该数字四舍五入到最接近的整数。）

如需了解 详细信息，请参阅 [DisplayMetrics](https://developer.android.com/reference/android/util/DisplayMetrics.html) 类。



来源：https://developer.android.com/guide/practices/screens_support.html