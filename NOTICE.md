# NOTICE

NQRust Fleet Manager
Copyright (c) 2026 NexusQuantum

## Licensing

This project is a derivative work of [Rancher Dashboard](https://github.com/rancher/dashboard).

The combined work distributed in this repository — NQRust branding, theme
system, structural changes, plus the upstream Rancher Dashboard code as
integrated here — is licensed under the **GNU Affero General Public License
version 3.0 or later (AGPL-3.0-or-later)**. The full text is in [`LICENSE`](./LICENSE).

The upstream Rancher Dashboard code is, and remains, licensed under the
**Apache License, Version 2.0**:

```
Copyright (c) 2014-2026 SUSE LLC, Rancher Labs Inc., and contributors
Licensed under the Apache License, Version 2.0
https://github.com/rancher/dashboard
```

A full copy of the upstream Apache 2.0 license is preserved at
[`LICENSE-APACHE-2.0`](./LICENSE-APACHE-2.0). All upstream copyright notices
and source headers remain intact in their original files. Apache 2.0 § 4
permits redistribution under different terms, and Apache 2.0 is one-way
compatible with AGPL v3 — the combined work moves to AGPL v3, while the
unmodified upstream files retain their original Apache 2.0 status.

## Modifications introduced by NexusQuantum

NQRust Fleet Manager differs from the upstream Rancher Dashboard in the
following ways. None of these modifications change the API surface, the data
contracts with the Rancher backend, or the extension authoring interface.

- A complete visual reskin (theme tokens, density, focus states) introduced via
  the cascade-final overlays at `shell/assets/styles/themes/_nqrust.scss` and
  `shell/assets/styles/themes/_nqrust-icons.scss`.
- Brand assets replaced under `shell/assets/images/pl/`,
  `shell/assets/brand/suse/`, and `shell/static/`.
- Vendor / product-name constants in `shell/config/private-label.js` set to
  "NQRust Fleet Manager".
- Vendor-facing UI strings in `shell/assets/translations/en-us.yaml` replaced
  for the small set that are visible product labels (window title, main-menu
  logo alt text, the `products.rancher` and `about.versions.rancher` entries,
  the welcome greeting). Resource names, CRD references, documentation links,
  and authentication-provider configuration strings remain unchanged because
  they refer to backend identifiers, not user-facing branding.
- Local-cluster identification mark: the cattle silhouette in
  `shell/components/ClusterIconMenu.vue` and
  `shell/components/ClusterProviderIcon.vue` replaced with a brutalist
  fleet-stack glyph.
- `index.html` window title, theme-color meta, splash-spinner styling, and
  Material Symbols Outlined webfont preload added.
- Repository metadata in `package.json`, `README.md`, and this `NOTICE.md`
  updated to reflect the NQRust Fleet Manager brand.

These modifications are © 2026 NexusQuantum and are released under the same
Apache License 2.0 as the upstream project.

## Third-party assets

- Google Material Symbols Outlined — Apache License 2.0,
  https://github.com/google/material-design-icons.
- All other third-party dependencies retain their original licenses; see
  `package.json` and the bundled `node_modules` for details.

## Trademarks

"Rancher", "SUSE", and related marks are trademarks of SUSE LLC. They are
referenced in this project only for the purpose of attribution and to describe
the upstream project. NexusQuantum does not claim affiliation with or
endorsement by SUSE LLC or Rancher Labs Inc.
