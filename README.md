VFX graph simulates raindrops sliding down, this is rendered by an extra camera into a render texture. Which is then used in a very simple fragment shader.
This shader constructs normal map of droplets from the grayscale texture. Which is the main bottleneck.

To optimize this, I would render this VFX into a sprite sheet and produce normal map of it offline. Then the effect would be free but no longer procedural.
I'm also sampling this render texture twice for normals and twice for smoothness to improve tiling. But this is not essential and can be freely removed.
I've solved obvious vertical tiling by adding a black gradient frame in the vfx graph.

VFX graph has spawn rate property exposed in the scene, change it in the inspector to get a different rain amount.

Memory cost: under 2 MB including shaders.
GPU cost: under 0.4 ms

Render texture is set to single channel 8 bit as I only render black and white. No depth, no anti-aliasing needed. 1024x1024 but 512 will be fine as well.