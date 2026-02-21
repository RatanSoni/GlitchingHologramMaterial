# Glitching Hologram Material — Unreal Engine

![Glitching Hologram Effect](Media/Glitching_Clip.gif)

A dynamic, highly customizable **Glitching Hologram Material** for Unreal Engine. Designed to give any static mesh a sci-fi, unstable holographic appearance using a hybrid approach that combines procedural math for scanlines and edge emission with texture maps to drive erratic glitching patterns. The result is a versatile material optimized for real-time rendering with extensive artist-friendly controls.

> **Portfolio Page:** [ratandsoni.weebly.com/glitching-hologram-material](https://ratandsoni.weebly.com/glitching-hologram-material.html)

---

## Features

- **Procedural Scanlines** — Math-driven horizontal scanlines with adjustable frequency, speed, and intensity.
- **Texture-Driven Glitch** — Erratic chromatic distortion patterns controlled via texture maps for organic, unpredictable results.
- **Edge Glow / Rim Emission** — Fresnel-based emissive rim highlighting for that classic hologram look.
- **Semi-Transparency** — Configurable opacity with holographic falloff.
- **Modular Architecture** — Built with reusable Material Functions for clean, scalable graphs.
- **Artist-Friendly Controls** — All key parameters exposed and organized into intuitive groups (Edge Glow, Glitch, Holographic) in the Material Instance.
- **Real-Time Optimized** — Designed for performant real-time rendering in games and interactive applications.

---

## Material Breakdown

### MF_CustomPanner

A reusable Material Function for custom UV panning with independent X/Y speed control.

- Takes base UVs from `TexCoord[0]` and splits them into R and G channels.
- Multiplies a time node by separate `SpeedX` and `SpeedY` scalar inputs.
- Adds the animated offset to each UV axis independently, then recomposes via `Append`.

---

### MF_Glitch

A Material Function that generates an animated glitch mask for UV distortion.

- Uses two instances of `MF_CustomPanner` with a shared `Glitch Speed` parameter to animate `LinearGradient` UVs.
- Pipes the gradients through `Sine → Sine → Cell` node chains to produce blocky, erratic patterns.
- Combines horizontal and vertical glitch patterns via `Add`.
- Multiplies the combined pattern by a `GlitchTexture` scalar and a `GlitchAlpha` intensity control.
- Outputs both the distorted UV offset and a mask for selective application.

---

### M_Hologram (Master Material)

The main hologram material that brings everything together. Key systems include:

| System | Description |
|---|---|
| **Scanlines** | Procedural horizontal lines driven by world position and time |
| **Edge Glow** | Fresnel-based rim emission with adjustable power and color |
| **Glitch Distortion** | UV offset from `MF_Glitch` applied to base texture sampling |
| **Color & Emission** | Holographic tint with emissive intensity controls |
| **Transparency** | Configurable opacity blending with glitch-driven alpha variation |

---

### MI_Hologram_Inst (Material Instance)

A ready-to-use Material Instance of `M_Hologram` with all parameters organized into groups:

- **Edge Glow** — Rim color, power, intensity
- **Glitch** — Glitch speed, alpha, texture influence
- **Holographic** — Base color tint, scanline frequency/speed, emission strength, opacity

Simply drag onto any static mesh to apply the hologram effect and tweak parameters in real time.

---

## Getting Started

### Requirements

- **Unreal Engine 5.x**
- Project with default starter content (or supply your own textures)

### Installation

1. **Clone** this repository:
   ```bash
   git clone https://github.com/RatanSoni/GlitchingHologramMaterial.git
   ```
2. **Copy** the `MaterialFunctions/` and `Materials/` folders into your Unreal project's `Content/` directory.
3. **Open** `MI_Hologram_Inst` and assign it to any mesh in your scene.
4. **Adjust** exposed parameters to taste.

> **Note:** The `.uasset` files are Unreal binary assets. To recreate from scratch, follow the node graphs shown in the [portfolio page](https://ratandsoni.weebly.com/glitching-hologram-material.html) or refer to the material breakdown above.

---

## Author

**Ratan D. Soni** — Technical Artist & Developer

- Portfolio: [ratandsoni.weebly.com](https://ratandsoni.weebly.com)
- GitHub: [github.com/RatanSoni](https://github.com/RatanSoni)

---

## License

This project is licensed under the [MIT License](LICENSE).
