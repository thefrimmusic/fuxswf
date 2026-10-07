# Wormhole Lab

![All 15 modes](modes-preview.png)

Audio-reactive tunnel visuals for DJ sets, built around the 1997 *Contact* wormhole ride (Weta Digital) and a dithered "we must go deeper" spiral GIF. One self-contained WebGL2 page with no build step and no dependencies.

## Run it

- **Hosted:** open the published page. Load a track from the Audio panel, or drop an audio file anywhere on the page.
- **Locally, with mic or line-in:** browsers only allow the mic on a secure origin, so serve the folder instead of double-clicking the file:

  ```sh
  cd wormhole-lab && python3 -m http.server 8000
  # then open http://localhost:8000 and press "Use mic or line-in"
  ```

## What's in it

**15 tunnel modes:** Contact '97, Deeper, Bloodstream, Nexus, Circuit, Contact: Amber, Neon Gates, Hex Gates, Mercury, Fractal Cathedral, Stargate '68, Hyperspace, Lawnmower '92, Demoscene '93, XOR '91.

- *Contact '97 / Amber*: a volumetric raymarch through domain-warped fractal noise, streaked along the direction of travel, with ridged-noise "lightning".
- *Bloodstream / Circuit*: a real 3D maze. The shader carves tubes on a lattice using a hash, and a JavaScript random walk runs the same hash (`segOpen` ↔ `segR`), so the camera only turns into tubes that are actually open.
- *Nexus*: the main tunnel cuts through both labyrinths of a gyroid, so side passages weave around it everywhere.

**7 looks**, any of which works with any mode: Clean, Film '97, GIF dither (blue-noise stipple, like the screenshot), 1-bit, VHS, Thermal, Acid.

**Membrane punch-through:** a rippling sheet of liquid light (or mirror, or grid) spans the tunnel, rushes at the camera and bursts with a flash and a shockwave. It fires on Punch, every N bars, on detected drops, and between modes in Auto VJ.

**Audio:** kick detection uses spectral flux on 35–130 Hz with an adaptive threshold, and the BPM is the median of the gaps between kicks. Each band has its own auto-gain. The kick drives speed surges, flashes and light waves; the sub makes the walls breathe; hats add sparkle. A 122 BPM ghost beat keeps things moving when nothing is playing.

## Nexus Runner (`nexus.html`)

![Nexus Runner mid-detour](nexus-preview.png)

A visualizer built only around the Nexus tunnel. You ride the main tunnel, and every so often the camera turns off into one of the side arteries, threads through the gyroid labyrinth junction by junction, and finds its way back to the main line.

- **Real side paths.** The arteries are the two labyrinths of the gyroid. Their junctions sit at odd multiples of π/4, where g = ±1.5, and each one has exactly three branches. The route planner walks that graph and checks every turn-off and rejoin against the same distance field the shader draws, so the camera never cuts through a wall. Across 12+ simulated minutes and about 900 junctions, it never got closer than 0.12 units to a wall.
- **When it turns off:** every 8, 16 or 32 bars, on the drop, or when you press **Detour** or `Space`. **Lost** keeps it wandering almost all the time. Detour length can be Short (2–3 junctions), Medium (3–6) or Long (6–11).
- **What you see:** each kick sends a ring of light out through the labyrinth from where you are. Arteries widen around the camera as it passes, the view widens inside them, and each junction you pass flashes. A route map shows the main line, your trail colored by labyrinth, and the path ahead.
- 5 palettes (Nexus, Ember, Biolume, Ultraviolet, Ghost), the same 7 looks as the Lab, and the same audio engine.

## Keys

`Space` punch through · `←` `→` change mode · `1`–`9` jump to a mode · `L` cycle looks · `A` toggle Auto VJ · `H` hide controls · `F` fullscreen · drag to look around · tap to hide or show the controls.

Quality is adaptive: the scene renders at a reduced resolution that scales with the measured frame rate, then gets upscaled. You can pin Low, Medium or High in Tune.
