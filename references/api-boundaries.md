# ResolveMCP integration

Checked against server-supplied Resolve 21.1 API stubs on 2026-10-01. These are documentation findings; refresh for the connected build before execution. The installed server is `davinci_resolve`. Do not invoke Samuel Gursky's `timeline_item_color`, `safe_set_cdl` or advanced offline tools unless they are actually installed.

## Discovery and execution

Use `get_resolve_status` and `get_whats_new`, then `search_scripting_api` for a focused topic. Fetch relevant types through `get_scripting_api`; use `get_scripting_docs` for semantics. `run_script` injects `resolve` and `project`; assign structured output to `result`.

These names describe the inspected server, not guaranteed tools on every installation. Discover the connected server first; report missing tools or state instead of inventing equivalents or opening an arbitrary project.

| Surface confirmed in supplied stubs | What still needs verification |
|---|---|
| `Timeline.GetSelectedClips` | Selected timeline objects versus playhead clip |
| `TimelineItem.GetCurrentVersion`, `AddVersion`, `LoadVersionByName` | New version preservation and active version after creation |
| `TimelineItem.GetNodeGraph(layerIdx)` | Correct node-stack layer and write targeting |
| `Graph.GetNumNodes`, `GetNodeLabel`, `GetToolsInNode`, `GetLUT` | Empty tool/label information cannot prove neutral CDL |
| `TimelineItem.SetCDL` | Existing values, effect on chosen layer, actual rendered result |
| `Project.ExportCurrentFrameAsStill` | Output encoding and visible processing on this build |
| `Timeline.GrabStill` | Gallery creation is a mutation; export method and recovery fidelity |
| `Graph.ApplyGradeFromDRX` | Whole-grade replacement risk, correct target and recovery |

`CDL` accepts integer `NodeIndex` (1-based), space-separated RGB strings for `Slope`, `Offset`, `Power`, and floating-point `Saturation`. The supplied type marks fields optional, but omission semantics must be verified before relying on them to preserve an existing grade. No `GetCDL` or node-enabled getter was found in the supplied Graph/CDL API. Do not invent them.

`GetNodeGraph(layerIdx)` identifies a graph for inspection; it does not select the write layer. `TimelineItem.SetCDL(CDL)` has no layer argument. Before writing, establish its target-layer semantics from connected-build documentation or an authorized isolated disposable test. If unresolved, stop the write and offer a verified UI route or manual instructions.

The graph does not directly expose new-node creation or detailed Color-page wheel, curve, qualifier/window or OFX parameter setters in this snapshot. Refresh the API before declaring a future build unsupported. If using UI automation, inspect current UI state through the available computer-use workflow. Without that capability, provide concrete manual steps and stop the unsupported operation.

## Verification contract

Read version, target and graph state before/after when accessible. A successful CDL return establishes that Resolve accepted the request; unchanged node count does not prove unchanged grading controls. Verify rendered output separately. Record supplied numeric values as the operation log, not as values read back from Resolve.

Before editing, record the original version name/type or recovery artifact, target identity and exact restore operation. Accept recovery only when documentation for the connected build or an authorized isolated disposable test establishes preservation of the affected grade state. A version name, unchanged node count or one matching frame does not prove whole-grade preservation. Confirm recovery creation succeeded and the intended working version is active. Stop if preservation or restoration remains unknown; do not test unfamiliar recovery on the user's only baseline.

A duplicated timeline may still use shared nodes or remote grades: it is not automatically an isolated color backup. Stop if an action's affected scope cannot be established. Disposable tests themselves require authorization; a review request does not authorize creating test versions or projects.

The LUT/DCTL creation tools produce assets; that alone does not prove installation on the target node or visible effect. Distinguish asset generation, application and rendered verification in the handoff.
