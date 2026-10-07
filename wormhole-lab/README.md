# Wormhole Lab

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

## Keys

`Space` punch through · `←` `→` change mode · `1`–`9` jump to a mode · `L` cycle looks · `A` toggle Auto VJ · `H` hide controls · `F` fullscreen · drag to look around · tap to hide or show the controls.

Quality is adaptive: the scene renders at a reduced resolution that scales with the measured frame rate, then gets upscaled. You can pin Low, Medium or High in Tune.
