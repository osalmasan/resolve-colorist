# Color workflow

## Establish the image pipeline

Record known source gamut/gamma or RAW decode, project color science, timeline working space, clip input override, CST/LUT placement, group processing, timeline grade and output transform. Read relevant settings only. A pipeline may be managed by RCM/ACES, explicit transforms, or a combination: diagnose it before inserting another transform.

ACES defines distinct input, look and output transforms; the output transform renders scene values for the intended display. Preserve the active project's implementation and version. Do not assume a LUT takes camera log, or that every CST is an output transform. [ACES output transforms](https://docs.acescentral.com/system-components/output-transforms/)

## Evidence record

For each target capture this compact record:

```text
Target: project / timeline / clip ID / timecode / version / layer / node
Pipeline: source -> working space -> look -> output; unknowns
Picture: visible issue and subject that must be protected
Scopes: measured values and scale, or unavailable
Intent: correction or desired mood; reference provenance
Recovery: original version name/type or artifact, preservation evidence, restore operation
Change: operation, absolute values if known, affected scope
Review: before/after frames, adjacent shots, unresolved issues
```

Use exported Resolve frames as visual evidence. A thumbnail may omit processing; test the capture method on the installed build. Record image encoding and export/view transform. Do not merely label log/HDR pixels sRGB. If only an SDR preview of HDR is available, judge composition and relative appearance, but reserve HDR highlight approval for an appropriate display/output check.

For each capture, confirm the target clip and frame, record the page/timecode and viewing state before navigation, and export to a unique scratch path. Verify export success and file existence, then actually open and inspect the image. Compare the same frame and known output/view transform; if either is unknown, qualify the comparison rather than claiming visual validation. Do not substitute Gallery creation for a read-only export.

Use waveform for tonal placement, RGB parade for channel relationships and vectorscope for chroma/hue where available. A whole-frame RGB imbalance does not establish a cast in a colored scene. Do not invent readings from a screenshot too small to read. Scopes and stills are supporting evidence, not an automatic aesthetic score. [Blackmagic Color](https://www.blackmagicdesign.com/products/davinciresolve/color)

## Recovery and iteration

Adopt Samuel Gursky's central pattern: inspect pictures, preserve the current grade, apply a scoped change, compare results. Treat DRX and grade copies as potentially replacing the full grade. Never use a clean diagnostic reference as permission to erase the creative baseline. [Color decision guide](https://github.com/samuelgursky/davinci-resolve-mcp/blob/main/docs/guides/color-decision-guide.md)

Before temporary bypass, record the actual original enabled states and ensure they can be restored. If the API cannot read those states, do not guess that all nodes were enabled. Prefer an existing verified reference version. Keep normalization/output transforms active for useful comparisons; raw log versus a rendered grade is not a like-for-like creative comparison.

On success or failure, restore recorded temporary navigation, viewing, bypass and diagnostic-version state; leave the authorized final grade active after an edit. Do not guess unreadable prior states or overwrite intervening user changes. Report any cleanup failure and the remaining state. Recovery acceptance and write-layer checks are defined in [API boundaries](api-boundaries.md).

For each pass, identify one priority and the expected visible improvement. Apply a modest adjustment, capture the same frame, evaluate, and retain or revert. Repeated unsuccessful passes are a reason to reassess the diagnosis, transform or tool choice. Broaden to the remaining requested shots only after the hero result is useful.

A finishing review covers meaningful temporal variation: exposure changes, movement through mixed lighting, noisy shadows, saturated practical lights, gradients, and adjacent cuts. Report sampling coverage; a few inspected frames do not certify the whole sequence.
