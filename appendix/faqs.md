# FAQs

## Volumetric Cloud Shimmer & Noise

### Runtime

{% file src="../.gitbook/assets/20260916-1837-54.2198076 (1).mp4" %}

If you see a shimmering artifact in the distant clouds when moving the camera up or down, this is likely caused by a low step count stepping over the LOD transtions. This is a performance saving measure, but has the tradeoff of reduced quality. If your project has rapid elevation gain or occurs in the clouds, you may want to adjust your settings to have a higher step count and a lower LOD coefficient.

### In Editor

{% file src="../.gitbook/assets/20260921-1653-10.0940782.mp4" %}

Volumetric Cloud TAA is linked to individual camera's in the scene to allow different cameras to render the same clouds from different angles. This uses URP's [CameraHistoryItem](https://docs.unity3d.com/Packages/com.unity.render-pipelines.core@17.2/api/UnityEngine.Rendering.CameraHistoryItem.html) so that the Render Graph handles the resources directly. A side effect of this, is that TAA is limited to only function for runtime cameras and it does not show in the scene view.

You may notice flickering and noise in the distance in the scene view as a side effect of this. This _will not appear in the game view_.
