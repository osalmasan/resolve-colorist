---
name: resolve-post-production
description: Use when working in DaVinci Resolve on color grading, exposure, white balance, color casts, shot matching, reference looks, or look development through ResolveMCP. Also applies to reviewing existing grades and nodes. Does not cover general timeline editing or video generation.
---

# Resolve Colorist

Develop a coherent look while retaining the user's creative baseline. Use the installed ResolveMCP and discover its current API. This skill prioritizes color work; the historical package name remains stable.

## Read for the task

- Every grading task: [color workflow](references/color-workflow.md).
- Exposure, neutral balance, or a cast: [exposure and balance](references/exposure-balance.md).
- Creative direction, reference images, shot matching, LUTs: [look development](references/look-development.md).
- Before scripting a mutation: [API boundaries](references/api-boundaries.md).
- To refresh domain knowledge or explain provenance: [sources](references/sources.md).

## Operating contract

1. Classify the request as review, technical correction, shot match, or look development. Follow its authorized scope; a review does not authorize edits.
2. Check Resolve status and changelog. Identify the exact project, timeline, clip IDs, current grade version, node stack/layer, and target node. Selection and the clip under the playhead can differ. Resolve any consequential ambiguity before writing.
3. Establish source encoding, working space, transforms and output intent. Missing camera metadata is unknown; never infer S-Log3 from a Sony filename. Inspect representative Resolve-rendered frames and available scopes. Separate observed facts from inferred causes.
4. Explain the intended visible change briefly. Protect the existing grade with a verified recovery point. Check version creation/copy semantics; a new version name alone does not prove a backup. For shared nodes or remote grades, establish the actual affected scope.
5. Apply a bounded correction through a supported surface. Existing-node CDL writes set values; they are not guaranteed additive adjustments. Never fill unknown existing controls with neutral defaults. Use the API reference for argument types and node/layer targeting.
6. Compare matching timecodes and the intended output transform. Check the subject, adjacent cuts, highlights, shadows, hue and saturation. Inspect multiple frames when illumination or motion changes. Restore temporary viewing state when safe.
7. Report target/version/node, change, recovery, frame evidence, limitations and remaining review. Distinguish execution success, state verification and visual judgment. If numerical readback is unavailable, say so.

## Boundaries

Use `run_script` by default. Files exported through supported Resolve methods do not automatically require `run_script_unsafe`; use that only for actual OS access. Keep analysis files in session scratch, away from source media.

Do not replace graphs, change project-wide color management, or propagate a grade merely to achieve a local correction. Use those actions only when the request covers that scope. Stop after an ambiguous mutation timeout and inspect before retrying.

If frame capture or essential state is unavailable, provide a concrete diagnosis or adjustment proposal and identify the missing evidence. Never claim a look was visually validated from metadata, API success, or an unviewed image.
