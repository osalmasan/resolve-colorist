---
name: resolve-post-production
description: Use when working in DaVinci Resolve on color grading, exposure, white balance, color casts, shot matching, reference looks, or look development through ResolveMCP. Also applies to reviewing existing grades and nodes. Does not cover general timeline editing or video generation.
---

# Resolve Colorist

Develop a coherent look while retaining the user's creative baseline. Use the installed ResolveMCP and discover its current API.

## Read for the task

- Every grading task: [color workflow](references/color-workflow.md).
- Exposure, neutral balance, or a cast: [exposure and balance](references/exposure-balance.md).
- Creative direction, reference images, shot matching, LUTs: [look development](references/look-development.md).
- Before any grade mutation, including UI work: [API boundaries](references/api-boundaries.md).
- To refresh domain knowledge or explain provenance: [sources](references/sources.md).

## Operating contract

1. Classify the request as review, technical correction, shot match, or look development. A review does not authorize grade edits, version creation or Gallery stills; unique local scratch frame exports are allowed unless the user prohibits writes. For review, skip steps 4–5.
2. Discover available tools and check Resolve status and changelog. If the connection, running application, project or timeline is missing, report it; launch/open only within the request, never guess a project. Identify project, timeline, authorized clip IDs, current version, node stack/layer and target node. Selection and the playhead clip can differ.
3. Establish source encoding, working space, transforms and output intent. Missing camera metadata is unknown; never infer S-Log3 from a Sony filename. Inspect representative Resolve-rendered frames and available scopes. Separate observed facts from inferred causes.
4. Explain the intended visible change briefly. Require verified preservation semantics, a recorded recovery version/artifact and an exact restore procedure, as defined in the API reference. Stop if recovery or shared-node/remote-grade scope is unknown.
5. Apply a bounded correction through a supported surface with verified write targeting. Reading a graph layer does not select the layer for `SetCDL`. CDL writes set values, not guaranteed additive adjustments; never replace unknown existing controls with neutral defaults.
6. For edits, compare before/after at matching timecodes under the intended output transform; for reviews, assess the existing grade. Check the subject, adjacent cuts, highlights, shadows, hue and saturation, sampling motion or lighting changes. Follow the color workflow's cleanup protocol on success or failure; leave the original grade active after review and the authorized final grade active after editing.
7. Report target/version/node, change, recovery, frame evidence, limitations and remaining review. Distinguish execution success, state verification and visual judgment. If numerical readback is unavailable, say so.

## Boundaries

Diagnostic bypass or version switching requires authorization and recorded restorable state; a review request alone does not authorize it.

Use `run_script` by default. Files exported through supported Resolve methods do not automatically require `run_script_unsafe`; use that only for actual OS access. Keep analysis files in session scratch, away from source media. Use unique, non-overwriting artifact names; external uploads require authorization.

Do not replace graphs, change project-wide color management, or propagate a grade merely to achieve a local correction. Use those actions only when the request covers that scope. Stop after an ambiguous mutation timeout and inspect before retrying.

If frame capture or essential state is unavailable, provide a concrete diagnosis or adjustment proposal and identify the missing evidence. Never claim a look was visually validated from metadata, API success, or an unviewed image.
