# blender-shader-fluo

This procedural shader simulates a UV blacklight, and the emission effect it generates on fluorescent materials.

Works with both cycles and evee rendering engines.

Not perfect, c.f. caveats below.

![stability - experimental][experimental-img]


## Demo

[images to be added here]

## Usage

Assuming `shader-fluo.blend` is downloaded in your computer.

1. Use Blender's `File \ Append` feature in order to add the following to your scene:
  * `blacklight` object
  * `shader-fluo` node group
2. Select the object you want to make fluorescent, and go to the Shader editor.
  * Add the `shader-fluo` node group.
  * Connect its output to the material output
  * Connect a shader for the non-fluorescent effect to the `base-material` input. Typically, a Principled BSDF, or a Diffuse BSDF.
  * Define the fluorescent emission color inside the `Color` input.
  * Adapt the following **parameters** as suitable:
    * Position of the blacklight in the scene
    * Power of the blacklight
    * Scale value of the `shader-fluo` node group - extra control over lamp's power and distance.
    * Intensity value of the `shader-fluo` node group - controls the fall-off effect.
  

Basic setup looks like this:

![demo 1](img/simple-shader-setup.png?raw=true)

### Pro-tips

* If you aim at realistic fluorescense, you may want to use a `Wavelength` to set the fluorescent emission color.
* The blacklight's color does not affect the fluorescent emission effect. Set it to lack in case you do not want it to emit visible light at all. The fluorescent emission will still happen, as long as the light's power is greater than zero.

## Approach

A regular point light is used as the black light.
A node group determines a material's fluorescence according to the distance between the object's surface and the lamp, plus some variables

### Benefits

* Black light can be combined with regular lights.
* Fluorescent color emission can be controlled by the blacklights' position and power - and animated.
* Objects have a regular color reacting on regular light, and independent from the fluorescent emission.
* Control fluorescence per material, and not for the whole scene.
* Works in Cycles.

### Caveats

* The UV light must be a point. and emits light spherically
* The UV light is not blocked by any obstacle, and can therefore produce non-realistic results

### Alternative techniques

Other approaches can be found in the wild:

* Use a `Shader to RGB` node, as demonstrated by Lemon in this [stackExchange answer](https://blender.stackexchange.com/a/148893/93500) - Eevee only.
* Use [ Ultimate Blacklight Shader for Blender Eevee ](https://gumroad.com/l/yVRmi) addon by Axiom Design ($2+) - Eevee only.
* Render the fluorescent surfaces as fully transparent, and use an `AlphaOver` node in the compositor editor to add color. As demonstrated by Uncreative Guy in [this video](https://www.youtube.com/watch?v=67NRNxJu8h8).

## License

This creation is provided under a Creative Commons Attribution license (CC BY). Please read [LICENSE.md](LICENSE.md) for more details.

Licensor: Mehdi El Fadil, Alcove design.


[experimental-img]: https://img.shields.io/badge/stability-experimental-orange.svg?style=flat
