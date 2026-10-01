# Exposure and color balance

## Diagnose before choosing a control

Distinguish exposure from contrast, a color cast, wrong levels, a missing transform or display mismatch. A low-key image need not be lifted. A dark face against a bright window may need selective work rather than a global lift. Preserve intentional lighting and product colors.

For an exposure request, locate the subject, useful shadow detail and important highlights. Describe the target in picture terms, such as a clearer face while retaining window detail. Do not impose one skin IRE value across skin tones, lighting, transfer functions or delivery formats. Clipped source detail cannot be recreated by lowering brightness; first determine whether clipping arose in capture or downstream processing.

For white balance, use a credible neutral under the subject's light when one exists. Reflections, tinted walls, specular highlights and colored practicals are unreliable neutral references. In mixed lighting, select the subject/light to prioritize and explain why a global adjustment may not solve both regions.

## Choose a tool based on value space

Blackmagic's primary wheels, log controls and HDR tools have different tonal behavior. Their availability in the UI does not establish scripting access. Use UI-assisted controls when available and appropriate, following the installed computer-use skill. [Blackmagic Color](https://www.blackmagicdesign.com/products/davinciresolve/color)

For a proven scene-linear signal, an exposure change of E stops is multiplication by 2^E. Do not apply this multiplier directly to S-Log3, DaVinci Intermediate, ACEScct, sRGB or another nonlinear encoding and describe the result as calibrated stops. Identify the node's actual input encoding. A CDL slope adjustment in an unknown space is a brightness/balance adjustment with visually assessed strength, not a known stop change.

ASC CDL uses slope, offset, power and saturation. Conceptually, SOP processes `(input * slope + offset)^power`; clipping and negative-value handling depend on implementation/style. These terms are not interchangeable with Resolve Lift/Gamma/Gain UI values. [OpenColorIO CDL reference](https://opencolorio.readthedocs.io/en/stable/api/transforms.html)

| Intent | Possible route | Verify |
|---|---|---|
| Broad brightness change | Equal-channel SOP, after space and baseline checks | Subject visibility, channel clipping, shadow noise |
| Neutralize a cast | Small RGB SOP differences in an identified correction node | Neutral under chosen light, skin and product hues |
| Shape density | SOP for broad changes; curves/HDR for finer work | Black detail, midtone separation, highlight texture |
| Selective face/sky correction | Supported UI window/qualifier controls | Matte, edges and tracking across motion |
| Reduce excessive chroma | Saturation trim | Important colors and adjacent-shot consistency |

Neutral CDL is slope/power `1 1 1`, offset `0 0 0`, saturation `1`. These are explanatory reference values, never a default payload for an already-graded node. CDL saturation `1` is not Resolve's UI saturation `50`.

`SetCDL` assigns values. If the existing CDL cannot be read, do not estimate an additive correction by writing a neutral-based full payload. Preserve a recovery version, then either use a verified neutral correction node or obtain authorization to replace the selected node's CDL values. For a neutral node, first verify its role and position relative to CST/LUTs. A label like “Balance” alone proves neither neutral values nor the signal encoding.

After balancing, compare with the baseline at the same timecode. Watch for an accidental magenta/green shift, changed skin saturation, contaminated blacks, and channel clipping. Review the nearby cut before declaring the correction matched.
