# Nexus Terminal Forge — v0.1.0-alpha.7

**One-file Nexus publisher + one-file AI Prompt Studio.** Made by @Z0M8I3D / DigiMancer3D.

This is a public alpha. Generated terminals use a cinematic seven-layer design, curated project worlds, creator artwork, GitHub public image discovery, locally owned visitor `.udata`, and per-project / creator share capsules.

## Open

Extract the ZIP into a fresh directory, then open `Nexus_Terminal_Forge.html` or `index.html`. There is no build tool or installer. The generated single-file `index.html` contains all CSS and JS. For a local server (recommended for consistent browser networking), from that directory:

```bash
python3 -m http.server 8787
```

Open `http://localhost:8787` in LibreWolf, Firefox or Chromium. **Do not confuse running locally with a public host.** The origin-dependent experimental hashlinks require that the final Nexus is actually deployed at a stable HTTPS URL (for example GitHub Pages). Put that address in **Identity → Published Nexus URL**. A public website can also use its own current URL when that field is empty.

## Creator workflow

1. Enter GitHub handle, creator name, website, published Nexus URL, and optional related accounts.
2. Discover and select repositories or create manual projects.
3. Customize appearance and edit the project-world assignment pool.
4. Drag the center separator (or use Left/Right arrow keys while it has focus) to change editor/preview widths. Double-click it to reset. The divider width persists locally **as an interface preference only**, without auto-saving project content.
5. Preview, export standalone HTML, and optionally save `.nexus.json` for later editing. You can re-import the exported HTML.
6. The generated site defaults to public GitHub image discovery **ON**; visitors can disable it in Settings, and an explicit saved preference takes precedence.

Project rows wrap at narrow editor widths instead of hiding their Edit, Move Up or Move Down controls behind a horizontal scrollbar.

## Sharing: two real, distinct codecs

**01. IB V2 gzip (standard-compatible):** The visitor selects **Share project capsule** in a project sheet or **Share creator capsule** near the About footer. The site creates a small read-only HTML document and compresses it with native `CompressionStream('gzip')`; it verifies the bytes after `DecompressionStream('gzip')`, then produces an itty.bitty-style URL beginning `https://itty.bitty.app/#/data:text/html;format=gz;base64,`. That HTML opens independently if the public itty.bitty service is available and accepts the fragment. The browser never submits the capsule's contents as a URL query to this generator. The itty.bitty host itself is third-party and is outside our control. See the [itty.bitty specification](https://github.com/arfct/itty-bitty/wiki).

**02. NXSM1 experimental SPX/MRPS-inspired hashlink:** An independent, versioned **byte-oriented demonstrator**, not the verified reference SPX or MRPS implementations. It uses bounded runs (with binary A|a awareness) and byte backreferences, chosen with a finite-horizon minimum-recipe dynamic program. Its payload format is `NXSM1` magic + original length (LE u32) + FNV-1a checksum (LE u32) + path tokens. Encodes up to 48 KB of UTF-8 capsule JSON. The decoder is part of the published Nexus HTML, which opens a **read-only capsule screen**, avoiding an external codec service. The URL is `https://PUBLISHED_NEXUS/#nxsm1=BASE64URL`. The tested sample must reconstruct byte-for-byte and pass integrity checks before a link is offered.

**Experimental warning:** NXSM1 is **UNVERIFIED** as SPX/MRPS research. It is not the complete SPX Reflection Wheel token grammar, not the reference MRPS solver, not authenticated or encrypted, and no compression benefit over gzip is guaranteed. FNV-1a detects accidental corruption; it is not a cryptographic integrity guarantee. Run the included vectors and add further tests to develop evidence. The share dialog compares **gzip vs NXSM1 on the same JSON input**, separately from the final gzip-HTML IB2 link length. The two hashlink lengths are not apples-to-apples compression ratios because their content format differs.

Long URLs may be truncated by chat, QR and social systems. Share UI warns when they exceed 3,900 characters. An alternative **Download independent HTML capsule** option is provided.

## Security and constraints

- Inputs and manifests are validated; no third-party source code is executed during import.
- Capsule content is escaped before rendering. The experimental viewer is read-only and does not execute payload JS.
- Browser `CompressionStream` and `DecompressionStream` support is required for IB2 gzip creation; existing Nexus browsing continues without it.
- A successfully reconstructed test capsule is not proof of production safety or generally superior compression.
- Remote GitHub images, avatars, and repository discovery need internet access and can be affected by GitHub API limits.
- Hosting on GitHub Pages is static; it does not run Python/PHP server-side.

## Package contents

- `Nexus_Terminal_Forge.html` / `index.html` — standalone generator
- `Nexus_AI_Prompt_Studio.html` — standalone build-prompt generator, updated for both codecs
- `NostrDanish_44_Updated_alpha7.html` and `NostrDanish_67_Updated_alpha7.html` — updated imported examples
- `DEMO_Generated_Capsule_Nexus.html` — small generated showcase to test sharing
- `_terminal_template.html` and `development/nexus_share_module.js` — optional developer reference, **not needed to use Forge**
- `CODEC_TEST_VECTORS.json`, `TEST_REPORT.md`, screenshots, and `RELEASE_NOTES.md` — regression evidence and known limitations

The permanent open-source home is [Nexus Terminal Forge](https://github.com/DigiMancer3D/Nexus_Teminal_Forge). The footer credit uses **@Z0M8I3D / DigiMancer3D**.
