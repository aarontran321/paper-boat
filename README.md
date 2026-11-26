# Paper Boat

A paper boat bobbing on an open sea at golden hour, rendered in real time in a single WebGL2 fragment shader. No libraries, no build step, no textures: one `index.html`.

**Run it:** open `index.html` in a browser, or serve the folder (`python3 -m http.server`) and visit it.

## What's in the water

- **Waves**: 32 sharp-crested travelling waves with deep-water dispersion (`ω = √(g·k)`). Each wave drags the domain of the next, which bunches the small ripples onto the crests of the big swells.
- **Wave sets**: three slow, crossing modulations travel at roughly group speed. Where they line up, a set of big waves rolls through; elsewhere the sea goes quiet. Every page load (and **New sea**) picks fresh directions and phases.
- **Wake**: while the boat moves, the hull sheds a ring every 0.14 s. The rings overlap into a V-shaped wake with a foam trail, and the bow foam grows with speed.
- **Ray marching**: a coarse march brackets the first surface crossing, then a few secant steps refine it.
- **Optics**: Fresnel reflection of a procedural sky with clouds, a sun-glitter path on the fine normals, refraction down to a rippled sand floor with animated caustics, per-channel absorption (red dies first), and sunlight scattering through thin wave crests.
- **The boat**: 14 triangles, ray traced in the shader. They show up in direct view, in reflections, through refraction and from underwater. The paper glows when backlit, darkens where it's wet, and casts shadows on the water and the sea floor.
- **Physics**: the same wave function runs on the CPU. Damped springs drive heave, pitch and roll from the water height under the bow, stern and both sides. The boat slides down wave faces and drifts with the wind.
- **The lens**: each pixel starts on the front of the camera lens. When the lens dips into the sea, the frame splits at the waterline. Below it you get Snell's window, total internal reflection, light shafts and the hull seen from below.

## Controls

| | |
|---|---|
| **W / ↑**, **S / ↓** | sail forward / back |
| **A / ←**, **D / →** | turn (the camera swings in behind the boat) |
| drag left/right | orbit |
| drag up/down | raise or sink the camera (go underwater) |
| scroll | zoom |
| click the water | drop a ripple; nearby water pushes the boat |
| click the boat | poke it |
| **Dip the lens** | the half-in, half-out shot |
| **New sea** | reroll the swell |
| `H` | hide the UI |

Sliders set the sun's elevation (sunrise to midday), the swell height and the cloud cover. The resolution adapts to keep the frame rate smooth.

Inspired by a paper-boat water scene in a Claude artifact; this is an independent re-implementation.
