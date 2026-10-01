# Research and adaptation notes

Research date: 2026-10-01. These references inform original workflow instructions; no upstream skill bundle or server was installed.

- [Blackmagic Resolve Color](https://www.blackmagicdesign.com/products/davinciresolve/color): primary/log/HDR tools, scope-assisted assessment and available Color-page features. UI availability is distinct from scripting support.
- [Blackmagic training](https://www.blackmagicdesign.com/products/davinciresolve/training): official learning path covering color correction, advanced color and color management. The linked Colorist Guide is useful for further study; its PDF exceeded the browser fetch limit during this research and was not read.
- [Samuel Gursky color decision guide](https://github.com/samuelgursky/davinci-resolve-mcp/blob/main/docs/guides/color-decision-guide.md): frame-based decisions, recovery, preservation of existing creative grades and honest automation limits. Only the workflow pattern is adapted; this package uses the installed ResolveMCP API.
- [ACES look-transform specification](https://docs.acescentral.com/system-components/look-transforms/specification/): look transform input/output contracts and workflow placement.
- [ACES output transforms](https://docs.acescentral.com/system-components/output-transforms/): scene-to-display rendering and output-specific viewing context.
- [OpenColorIO CDL API](https://opencolorio.readthedocs.io/en/stable/api/transforms.html): SOP/saturation and implementation styles. This reference does not establish Resolve's exact clipping implementation.
- Installed ResolveMCP `search_scripting_api` and `get_scripting_api`, types `CDL` and `Graph`: parameter types and current automation boundaries.

The brief template, iteration strategy, evidence record and review criteria are recommendations designed for this user's skill. They are not claimed as industry standards or verbatim Blackmagic procedures. No universal camera profile, creative LUT, skin brightness target or output gamma is prescribed.
