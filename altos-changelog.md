# Altos Changelog
This page documents the changelog for Altos, the complete sky system for Unity. Altos is a game asset that enables you to integrate a procedural skybox, volumetric clouds, day night cycle, stars, and moon into your project.

<a class="os-custom-button" href="https://occasoftware.com/altos">Learn more</a>
<a class="os-custom-button" href="https://bit.ly/altos-occasoftware">Buy now</a>

## Changelog

### 3.1.0
*September 25, 2022*
- Depth Fog now renders before transparents and before the cloud pass. This should improve compatability with transparent objects in scene and should avoid inconsistent shading on opaque objects behind volumetric clouds. 
- Unclamped Depth Fog Start and End values, giving more flexibility over how depth fog appears in your scene.
- Periods of Day are now treated as Keyframes. The skybox will linearly interpolate from the current keyframe to the next keyframe. This gives more control over the skybox color settings and removes some bandaids included to compensate for the old approach.

### 3.0.0
*September 22, 2022*
#### Volumetric Cloud Improvements
* Improved volumetric cloud lighting and density methods. Clouds will now render more realistically and with greater detail.
* The Cloud Sun Color is now a Sun Mask Color. The clouds will use the scene sun color and multiply it by the mask color. This improves the rendering quality by improving the consistency of scene-cloud lighting.
* Cloud Render Texture sampling and upscaling is now performed using a dithered min depth coverage system. This helps to prevent incorrect depth samples from appearing in the Cloud Upscaling results. These incorrect depth samples would appear as black artifacts around scene objects, especially under camera or object motion.
* Removed the Custom render scale option. This option is incompatible with the new dithered depth coverage system.
* Local Rendering is now limited to Half or Full render scales.
* Skybox Rendering still supports Quarter, Half, or Full res render scales.
* Temporal Anti-Aliasing is now performed after upscaling. This helps the TAA texture retain higher-quality data from frame-to-frame and improves the final render quality.
* Ray Depth now correctly accounts for the ray direction. Clouds in the edge of the screen will no longer fade out of view early.
* Procedural cloud weathermaps are now generated with more octaves, leading to a higher degree of quality in weathermap coverage results.
* Replaced all Volume Textures with newly created higher quality Volume Textures and simplified the Volume Texture loading system. These Volume Textures also now support mipmaps.
* Clouds are now sampled using a mipmap approach; clouds further away will be sampled using lower-detail mip levels than those nearby.
* High Altitude Clouds now rendering using multiple sampling steps, resulting in high altitude clouds that appear more 3-dimensional. These clouds now also sample lighting through each of these steps, effectively mimicking the approach used by the real low altitude volumetric clouds
* Improved the Ambient Lighting model so that clouds now have more apparent depth and detail from ambient lighting.
* Improved the Outscattering Lighting model so that clouds now have more accurate outscattering light results.
* Improved the Direct Lighting model so that clouds now capture more light deeper into the cloud volume, yielding smoother and more realistic cloud lighting results.
* Improved the Inscattering Lighting model so that clouds now more accurately demonstrate the effects of in-scattering in dense regions.
* Improved the Fog Lighting model so that low altitudue and high altitude clouds are fogged according to a shared fog density property.
* Curl Noise will now be applied on both the xz and xy axes, resulting in improved curl definition and results.
* High altitude clouds sampling method has been adjusted. Before, you had 3 noise texturues that combined for the high altitude cloud covearge. Now, you have a Weathermap + 2 noise textures that erode from the weathermap for the final density.
* Adjusted Henyey-Greenstein methods to yield more consistent and realistic results.
* High Altitude Clouds are now sampled on their own cloud layer, adding parallax and depth to the cloud coverage.
* Additional various performance optimizations.

#### Sun Lamp and Day/Night Cycle Improvements
* The Sun Color is now set automatically by default based on the sun direction. The sun color and intensity is based on physically-based color temperature and intensity measurements. This improves the rendering quality by more closely replicating real light conditions based on the time of day.

#### Animated Skybox Improvements
* The Skybox Sun Color is now a Sun Mask Color. The skybox will use the scene sun color and multiply it by the mask color. This improves the rendering quality by improving the consistency of scene-skybox lighting.


#### Utilities and Demo Scene Improvements
* Added additional objects in the demo scene to help demonstrate the Cloud and lighting systems.
* Added a script that will monitor your trailing average frame timing to help you more easily track performance impact from various cloud features.
* Added an elastic bounce script that will automatically move some test objects in the demo scene to help observe various temporal artifacts.
* Renamed the folder that contains options to create various sky Definition assets from *Skies* to *Altos*.


### 2.2.0
*August 26, 2022*

#### Bug Fixes
* Skybox cloud speed will no longer increase indefinitely.

#### Improvements
* Volumetric Cloud lighting has been improved.
* Volumetric Clouds can now be controlled with a density curve.

#### Useful Additions
* Now includes a free camera script to simplify demo usage.

### 2.1.2
#### Bug Fixes
* Altos will now pull in a cloud volume even if it is only made available after an additive scene load.


### 2.1.1
#### Bug Fixes
* Updated Render Passes so that they no longer call the CameraColorTarget outside of the RenderPass itself.

#### Housekeeping
* Added a warning that will appear on versions of Unity prior to the 2021 LTS to help ensure users are aware when they are running Altos on an incompatible version of Unity.
* Renamed some Render Passes classes to more accurately reflect the function of each class.
* Removed now-unnecessary Version Defines from the Assembly Definition.


### 2.1.0
#### Major Update
* The Altos 2022 Major Upgrade starts with release 2.1.0.

#### Editor Version Update
* Altos will now be mainlined against 2021 LTS. All future releases will target 2021 LTS.

#### Bug Fixes
* The cloud layer will no longer attempt to integrate with TAA Results during the first rendering frame. This improves first startup integration speed and screenshot quality.


### 2.0.0
#### Namespace Update
* Changed namespace to be more consistent with other OccaSoftware products, which use the following namespace format: OccaSoftware.Productname. The new namespace for the core functions for this asset is now OccaSoftware.Altos. The editor namespace is now OccaSoftware.Altos.Editor. I don't expect future breaking namespace changes in this or other packages. This release is labelled as a major change for this reason.

#### Bug Fixes
* Custom Passes within Altos no longer attempt to run during Reflection Probe camera passes. This resolves an issue causing Reflection Probes to return black when Altos custom passes were running.
* Removed an unnecessary Motion Vectors flag setting from the Volumetric Cloud Volume script resulting in Console Warnings.


### 1.11.4
#### Bug Fix
* Corrected a TAA rendering issue that would crop up when multiple viewports were open simultaneously in the editor.

### 1.11.3
#### Bug Fix
* Corrected a Render Texture sampling issue that was causing Motion Vector-based reprojection to swim or distort on the screen in some cases.

### 1.11.2
#### Bug Fix
* Corrected the Altos.Editor assembly definition so that Editor-only files are correctly excluded from builds.

### 1.11.1
#### New Features
* Introduced Procedural Weathermaps, which dramatically improve the overall structure of the cloud distribution. These come with new parameters to give you more control over your weathermaps, such as: Weathermap Velocity, Weathermap Scale, and Weathermap Value Range.
* Texture-based Weathermaps can now pan through space, with the introduction of the Weathermap Velocity parameter for Texture-based Weathermaps.
* Improved High Altitude Cloud Rendering
* Added another 2D Cloud texture that will now be the default for Skybox and High Altitdue Clouds.

### 1.10.1
#### New Features
* Introduced Camera Motion Vector-based Reprojection for Temporal Anti-Aliasing.

### 1.9.7
#### Bug Fixes
* Fixed an issue where the Render Features would attempt to execute even in scenes without a Skybox Director present. Going forward, Skybox Director must be present in any scene where you want any Altos Render Features to execute. These Render Features subscribe to the scene changed function and check the active scene upon change for their corresponding base class to be present (Star Object, Moon Object, Cloud Volume, Time of Day Manager). If the base class is not present at the time of scene load and is injected later, you will need to manually refresh the render features to ensure they pick up their references.
* Fixed an issue where distant clouds would pop out of view when entering the cloud layer from below. Distant clouds now render correctly at all times.
* Added VFX Graph define to eliminate errors experienced when importing Altos into a project where VFX Graph is not present. However, it is critical that you import VFX Graph first, before importing the Altos asset to your project. If you have imported Altos prior to importing VFX Graph, delete your OccaSoftware/Altos file path and re-import the asset so that VFX Graph can correctly configure the asset on import. If you do not do this, the asset will throw errors.
* Cleaned up all scripts to be correctly scoped within publisher namespace (OccaSoftware).

### 1.9.6
#### Bug Fixes
* Corrected a namespace access issue.

### 1.9.5
#### Bug Fixes
* Fixed a star, moon, and cloud rendering issue for URP 12+. Note that this fix comes with the introduction of an Assembly Definition for the Altos folder path.
* Fixed a type redefinition in the Clouds HLSL.hlsl definition that resulted in shader errors in Unity 2021.2+.

### 1.9.4
#### Bug Fixes
* Fixed a star rendering issue for Unity 2020.3+

#### Minor Adjustments
* Renamed Readme + Main Folder consistent with name change from Skies to Altos

### 1.9.3
#### Minor Adjustments
* Fixed cloud rendering issue for Unity 2020.3+
* Added Weathermap System.
 * This system enables users to dramatically increase level of detail of cloud data by predefing cloud "zones" and using volume textures to add detail. This is in contrast to the prior system, where the base volume texture itself was used to define cloud zones, thereby failing to fully take advantage of the value of the 3D texture data.
* Added RenderScale, Planet Radius, and Volume Channel Influence Falloff default options
* Sterilized tiling values for Skybox Clouds
* Added 6 new seamless tiling textures
 * 5 abstract noise textures (Clouds, Fire, Flower, Waves, Petals)
 * 1 Weather Map texture (Weather Map 1)
* Cleaned up file hierarchy
* Various performance improvements

### 1.9.2
#### Minor Adjustments
* Renamed from Skies to Altos
* Added in-scattering support for clouds
* Extended some editor options
* Slightly adjusted cloud modeling formulas
* Replaced the HG Forward/Back Blend term with an HG Max term that chooses the greater of the forward and back terms.
* Changed sun shape definition formula for skybox
* 3D Textures now correctly include an alpha channel

### 1.9.1
#### Minor Fixes
* Added horizon cutoff (clouds no longer render below the horizon)
* Clamped Henyey-Greenstein Coefficients to prevent clipping artifacts at high values
* Corrected High Altitude Cloud Rendering formulas
* Added lighting support for high altitude clouds

### 1.9.0
#### Revisited Volumetric Cloud Rendering Systems.
* Clouds now render using physically-based lighting and rendering algorithms.
* Clouds now are configured using a completely standalone editor using a Cloud Definition construct.
* Clouds come with 3 Volumetric Noise types (Perlin, Perlin-Worley, Worley) and 4 Volumetric Noise Quality levels (Low, Medium, High, Ultra)
* Clouds now supports low-altitude volumetric rendering with up to 3 levels of detail (Base, Detail 1, Detail 2) and high-altitude 2d rendering (3 textures) along with the pre-existing skybox cloud rendering (2 textures).
* Clouds also support Temporal Anti-Aliasing, full control over render scale (continous from 0.1x to 1x)
* Clouds now also support Skybox OR Local Rendering, allowing the clouds to be rendered in front of opaque objects in the scene.

#### Revisited Star and Moon Rendering Systems.
* Stars now render more accurately.
* The moon is now rendered in full 3d
* The moon  now supports physically accurate and controllable phases
* The moon is now rendered using a rendering pass within the Stars Rendering Feature. The Stars Rendering Feature now acts as a generic Celestial Bodies Rendering Feature.
* Stars are defined using a Star Definition object.
* Moon is defined using a Moon Definition object.

#### Performance Improvements
* Improved the performance of the Time of Day systems by moving several methods from Update to On-Demand functionality.

### 1.8.0
#### Feature Update
* Added controls that enable you to blend Volumetric Clouds with the Horizon to integrate with the Depth Fog functionality.
* Added parameters to give finer control over Volumetric Cloud alpha fadeout near the horizon.
* Added an Stars Rendering Feature that enables you to ensure Stars are always rendered behind Volumetric Clouds.

#### Housekeeping
* Cleaned up naming conventions in some Render Features.
* Updated readme docs to reflect these new functionalities.
* Cleaned up assets that were associated with features that were simplified to no longer require direct material references.
* Fixed terrain import data so that it includes layer data needed for the demo scene.

### 1.7.0
#### Feature Update
* Added one-click setup for the hierarchy and Time Of Day Manager configuration. It is now much easier to set up this asset in new scenes.
* Sun and Moon Lamp light configuration now uses light temperature rather than light color to enable more realistic lighting results. This is optional, but enabled by default, and can be switched back to using color by disabling the "use light temperature" option on each directional light.
* Moved Stars to a persistent game object. Stars will now appear in the Scene view.

#### Bug Fixes
* Fixed an issue that resulted when the Render Clouds command buffer shared the same command buffer designation as other render features.

### 1.6.0
#### Feature Update
* Added a Moon + Moon Shadowing support.
* Added horizon-blended fog into the Skybox.
* Added a Depth Fog image post effect, configurable from the Skybox Definition editor.
* Improved the quality of interaction between the Sun and the Volumetric Clouds.
* Updated file structure from Assets/Skies to Assets/OccaSoftware/Skies as per Unity Guidelines.

### 1.5.0
#### Feature Update
* Improved stars.

### 1.4.0
#### Feature Update
* The Skybox Definition inspector will now show you the current in-game time in hh:mm:ss format to enable easier debugging.
* The Skybox Definition inspector will now cache the Time of Day and retain it upon entering and exiting playmode.

#### Bug Fix
* Changes to your Skybox Definition will now be saved when exiting and re-launching the Unity Editor.
* Moved the "Volumetric Clouds Merge Pass" Shader into the /Shaders/Resources folder so that it is correctly included during a Build.

### 1.3.1
#### Bug Fix
* Volumetric Cloud Rendering now works in more recent versions of Unity.