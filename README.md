# Resolve Colorist

A Codex skill for DaVinci Resolve color balancing, exposure, shot matching and look development. Invoke it as `$resolve-post-production`. The displayed name is **Resolve Colorist**; the folder and invocation name retain the original project name.

It uses the ResolveMCP bundled with the user's DaVinci Resolve installation, registered here as `davinci_resolve`. Samuel Gursky's project inspired the workflow; its separate MCP server is not required.

## Current status

The package has been installed and discovered in Codex. Metadata and local reference links have been checked. Live grading validation is still pending.

## Requirements

- Codex with access to local skills and the ResolveMCP connection.
- A Resolve installation that supplies a working ResolveMCP. The API documentation inspected for this package was version 21.1; compatibility with other builds requires checking their available tools.
- An open Resolve project and timeline for live work, with the intended clip clearly identified.
- Accessible media. Supply camera gamut/gamma and intended output when known; unknown values should remain unknown until verified.

No extra Python packages, API keys or second Resolve server are required by this instruction-only skill. Individual tasks such as UI automation or media analysis can have additional requirements.

## Install the skill

Clone this repository into a folder matching the skill name:

```sh
git clone https://github.com/osalmasan/resolve-colorist.git resolve-post-production
```

Private repository access requires authentication with an authorized GitHub account.

The personal installation used for this package is `~/.codex/skills/resolve-post-production`.

For another machine, copy the entire `resolve-post-production` folder—including `agents` and `references`—into a personal skill directory recognized by that Codex installation. This setup uses `~/.codex/skills`. Use the configured Codex home if it differs. Do not install only `SKILL.md`.

From the directory containing the downloaded skill folder, this shell example creates a new installation and refuses to overwrite an existing one:

```sh
skill_parent="${CODEX_HOME:-$HOME/.codex}/skills"
if [ -e "$skill_parent/resolve-post-production" ]; then
  echo "Skill already exists; review the existing copy before updating."
else
  mkdir -p "$skill_parent"
  cp -R ./resolve-post-production "$skill_parent/resolve-post-production"
fi
```

For updates, compare the new package with the installed copy and preserve any local customizations before replacing files. A skill update does not require replacing the MCP configuration.

Start a new Codex task and check that `resolve-post-production` is available in the skill picker or by explicit invocation. If it is missing, check the directory nesting and `SKILL.md`, then restart Codex if needed.

## Check ResolveMCP separately

Installing the skill does not register an MCP server. This machine already has the connection configured. If the Codex CLI is available, `codex mcp list` shows configured servers; an enabled entry alone does not prove Resolve is reachable.

For a fresh connection, use the ResolveMCP setup instructions supplied with your installed Resolve build. Executable locations and setup requirements can vary. Avoid adding another server with the same name or installing Samuel Gursky's server just to use this skill.

Use this first prompt to verify live access:

> Use $resolve-post-production to check ResolveMCP connectivity and report the Resolve version, current project, timeline and selected clip. Do not edit anything.

If Resolve is closed or no project is open, open the intended project and retry. If Codex cannot find the tools, resolve the MCP connection first. The skill provides workflow instructions, not a connection by itself.

## First grading session

1. Open the intended project and timeline. Select the clip; place the playhead on a representative frame.
2. Start with an inspection prompt below. Confirm that Codex identified the right clip, grade version and node.
3. State the visible result you want and any colors or details to protect.
4. For an edit, let the skill establish a recoverable baseline and confirm the available operation.
5. Review matching before/after frames and nearby cuts in Resolve. Keep the version that serves your intent.

## How to prompt well

Name the target, desired appearance, constraints, and whether the request is review or execution. Add technical information only when you know it. A good prompt can be short:

> Use $resolve-post-production. On the selected clip, reduce the green cast and make the face a little brighter while retaining the window detail. Preserve my current grade in a recoverable version. Inspect the existing nodes and apply a supported correction, then compare before/after frames.

For precise work, use this optional template:

```text
Use $resolve-post-production.
Task: inspect / balance / exposure / shot match / develop a look
Target: selected clip, named clip, IDs or explicit timecode range
Node: number/label and stack layer if known; otherwise inspect first
Intent: the visible change and mood I want
Protect: skin, product colors, highlight detail, intentional lighting
Pipeline: camera gamut/gamma, working space, output if known
Reference: attached image or a specified shot; what to borrow from it
Scope: review only OR make the correction in a recoverable version
Review: matching before/after frames and the relevant adjacent cuts
```

“Cinematic” or “fix the color” alone leaves important creative choices unspecified. More useful direction describes density, palette and subject treatment: “slightly denser blacks with texture, warm highlights, restrained greens, and natural skin.” You do not need to specify CDL numbers.

## Prompt examples

### Inspect an existing grade

> Use $resolve-post-production to inspect the selected clip's color pipeline, exposure, balance and node graph. Identify the strongest issue and recommend an adjustment. Do not change the grade.

### Balance one node

> Use $resolve-post-production to reduce the unwanted green cast using node 3, labeled Balance, on the selected clip. Preserve the current look and create a verified recovery point. Inspect its existing values and role first. If the API cannot preserve those values, explain the available route before replacing them.

### Adjust exposure

> Use $resolve-post-production to improve the face's exposure on the selected shot while keeping the bright window and shadow texture. Keep the scene's low-key mood. Work in a recoverable version and verify several frames. Use calibrated stop adjustments only if the signal space and chosen tool support them.

### Develop a look

> Use $resolve-post-production to develop two reversible looks on the selected hero shot: a clean natural treatment and a warmer, denser treatment with restrained saturation. Keep skin and the product accurate. Test both on the brightest and darkest shots in this scene before proposing which one to extend.

### Match a reference image

> Use $resolve-post-production to use the attached image as a qualitative look reference. Borrow its soft highlights, cooler shadows and restrained palette while preserving this subject's skin tone. Check the image pipeline and explain which parts are achievable with the available controls. Develop a separate version and show the comparison.

### Match neighboring shots

> Use $resolve-post-production to match clips B and C to clip A's exposure and neutral balance within this lighting setup. Inspect the actual clips and existing grades first. Preserve each grade and apply individual corrections. Check the cuts for consistency; do not copy A's whole node graph.

### Continue or roll back

> Continue the current look: reduce its warmth slightly while keeping the contrast we chose. Use the same baseline and comparison timecodes.

> Restore the selected clip to the original grade version you recorded before this pass. Confirm the active version and compare it to the original frame.

Rollback depends on the recovery point actually established; the skill cannot reconstruct a lost original from a description alone.

## What automation can and cannot do

The inspected API supports setting CDL values on an existing node, accessing grade versions, inspecting parts of the graph, assigning LUTs and exporting frames. Each operation still needs correct targeting and current API verification.

CDL changes are absolute assignments. There was no CDL getter in the inspected API, so the skill cannot promise additive edits to unknown existing values or numerical readback. It protects the baseline, uses a verified correction surface, and judges the rendered result.

Color-page node creation, curves, qualifiers, windows, detailed wheels and OFX controls were not directly exposed in the inspected interface. Such requests may require UI-assisted work or a prepared grade artifact. Applying a DRX or copying a grade can replace the target grade. A LUT or CDL does not reproduce selective masks, tracked corrections, grain or a complete film-emulation treatment.

The skill should tell you what was changed, the recovery version, what frames were reviewed, and what remains unverified. Review stills are not a substitute for checking a finished sequence on an appropriate display.

## Package contents and sources

- [Skill instructions](SKILL.md)
- [Color workflow](references/color-workflow.md)
- [Exposure and balance](references/exposure-balance.md)
- [Look development](references/look-development.md)
- [ResolveMCP API boundaries](references/api-boundaries.md)
- [Research sources and attribution](references/sources.md)

For the distinction between skill instructions and MCP tools, see [OpenAI's skill documentation](https://developers.openai.com/plugins/build/skills).
