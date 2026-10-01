# Look development and shot matching

## Build a look brief

Translate the user's references or mood into observable choices. Fill only what matters for this job:

```text
Story/mood:
Reference images and their known encoding:
Subject and colors to protect:
Density/contrast: black texture, midtone weight, highlight softness
Palette: dominant hue relationships, saturation priorities
Texture: clean, grain, halation, diffusion; optional
Output/viewing target:
Tools needed and unsupported parts:
```

If the brief is vague, propose a restrained interpretation and develop it as a reversible variant. Request creative choice only when alternatives materially change the result. “Cinematic” alone does not authorize teal shadows, orange faces, crushed blacks or fake film grain.

## Develop on representative images

Choose a hero with the important subject and lighting. Also test a bright shot, a shadow-heavy shot, saturated colors and a different camera/lighting setup when present. Keep exposure/white-balance corrections separable from the reusable look wherever the existing graph permits.

Create clearly named versions such as `look-warm-v01` while preserving the baseline. For an open exploration, two purposeful alternatives are usually more useful than many barely different versions. Explain the perceptual difference rather than assigning an arbitrary “cinematic score.”

Compare references by specific attributes: density, shadow hue, highlight warmth, saturation distribution and subject/background separation. Respect differences in production design, light direction, makeup and skin tone. Histogram matching alone cannot reproduce those differences. If the reference encoding is unknown, call it a qualitative reference.

## Tool fit

- CDL: broad density, RGB balance and saturation proposals.
- LUT: a defined color mapping with known input/output spaces and domain. A LUT cannot carry spatial masks, tracking or grain.
- DCTL: a coded transform only after checking the supported DCTL language and actual node/application route.
- Existing DRX/PowerGrade: a complete grade artifact; inspect and protect the target before application.
- Curves, windows, qualifiers, texture and OFX: UI-assisted work or a verified prepared artifact when direct scripting is absent.

ACES look transforms have a defined scene-referred input/output contract; a display-oriented “film LUT” is not automatically interchangeable. Document the expected space and where a look belongs in the pipeline. Check whether an output rendering transform is already included to avoid applying it twice. [ACES look-transform specification](https://docs.acescentral.com/system-components/look-transforms/specification/)

A proposed logical order is input interpretation, shot correction, creative shaping, and output rendering. Adapt this to the existing managed pipeline and node order. It is a planning model, not authority to construct or reorder nodes.

## Match the sequence

Choose a reference shot per lighting setup. Compare the same subject and light, then balance exposure/density, neutral placement and saturation before refining the look. A shared look does not imply identical per-shot correction values. Do not automatically copy a hero's complete grade to clips with different transforms, masks or effects.

Review the actual cuts and moving footage when possible. Preserve motivated lighting changes between scenes. A sequence can be consistent without every shot having identical brightness or white balance.

## Acceptance

For each candidate, judge whether it communicates the requested mood and preserves important subjects. Check highlight separation, shadow visibility, skin/product color, gradients, saturation extremes and noise. Check more than one frame for spatial or temporal artifacts. Keep the winning version and recovery information; retain alternatives only when useful to the user.

Report the intended look, clips reviewed, output/view transform, exact remaining manual controls, and any unreviewed portions. Technical execution can be verified; final creative preference belongs to the user.
