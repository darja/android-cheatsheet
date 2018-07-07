# Android. UI

## Rotating Screen

In general, when screen is rotated, Activities are recreated. There are two ways to handle this situation:

* Using `configChanges="screenOrientation"` to activity manifest. In this case activity won't be recreated, but `onConfigurationChanged` method will be called, and we can handle this event there if needed. The issue of this approach is that we cannot use orientation-specific layouts automatically.
* Saving instance state in `onSaveInstanceState` in activities, fragments and views and restoring it again in `onCreate`. However, it is pain if you have many data to save.
* Using `ViewModel`, that can survive screen rotation

## Layout Process

## Bitmaps

## Drawables