# Android. UI

## Drawing the Layout

Views are organized as hierarchy. Views that can contain other views are called View groups and are derived from `ViewGroup` class. ViewGroups are rendered before their children.

Rendering views includes following steps:

* **Measure** — calculating desired size of the view. In custom views we should override `onMeasure` for that
* **Layout** — calculating position of child views
* **Draw**

## Rotating Screen

In general, when screen is rotated, Activities are recreated. There are two ways to handle this situation:

* Using `configChanges="screenOrientation"` to activity manifest. In this case activity won't be recreated, but `onConfigurationChanged` method will be called, and we can handle this event there if needed. The issue of this approach is that we cannot use orientation-specific layouts automatically.
* Saving instance state in `onSaveInstanceState` in activities, fragments and views and restoring it again in `onCreate`. However, it is pain if you have many data to save.
* Using `ViewModel`, that can survive screen rotation

## Bitmaps

`Bitmap` class represents a bitmap image.

### Loading Bitmaps

[Documentation](https://developer.android.com/topic/performance/graphics/load-bitmap)

In most cases we should use external libraries (Glide, Fresco, etc). If we cannot, we should use `BitmapFactory` with following steps:

* Read source image size and type (use `inJustDecodeBounds` flag)
* Define target size (e.g. `ImageView` measured size)
* Calculate scale factor, that should be power of 2
* Load bitmap again with `BitmapFactory`, using scale factor as `inSampleSize`

### Reusing Bitmaps

[Article](https://developer.android.com/topic/performance/graphics/manage-memory)

From Android 11 it is possible to reuse bitmaps instead of creating new ones for every image. It can be used with `BitmapFactory.Options.inBitmap` field. If this option is set, existed bitmap memory will be used instead of allocation/deallocation process.

## Drawables

[Documentation](https://developer.android.com/guide/topics/resources/drawable-resource)

**Drawable** is a concept for a graphic resource in Android. There are several types of drawables:

* **Bitmap** — wrapper for a graphic file (jpg, png, etc), providing some simple effects (tiling, stretching, etc)
* **9-patch** — png drawable with special format, that defing stretchable areas and areas for the content placement.
* **Shape** — basic way to define shapes with colors, strokes and gradients in XML
* **Level List** — composite drawable that includes different drawables, corresponding to some numerical values. Example usage: displaying rating image.
* **Layer List** — composite drawable that includes set of images
* **State List** — composite drawable that includes drawables for different view state (enabled, activated, etc)
* **Transition** — transition between two drawables
* **Clip** — a drawable that clips another drawable
* **Scale** — a drawable that scales another drawable
* **Inset** — a drawable that insets another drawable by a specified distance