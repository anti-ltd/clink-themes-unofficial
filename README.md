<p align="center">
  <img src="https://raw.githubusercontent.com/anti-ltd/clink-language-packs/main/icon-1024.png" width="96" alt="Clink app icon">
</p>

<h1 align="center">Clink themes — unofficial</h1>

<p align="center">Unofficial keyboard themes for Clink.</p>

Themes change the keyboard's colours, materials, type treatment, and gradients. They are ordinary JSON data, so you can read every setting before publishing a theme.

## Official Clink repositories

[Language packs](https://github.com/anti-ltd/clink-language-packs) · [Layouts](https://github.com/anti-ltd/clink-layouts) · [Profiles](https://github.com/anti-ltd/clink-profiles) · [Themes](https://github.com/anti-ltd/clink-themes) · [Panels](https://github.com/anti-ltd/clink-panels) · [Actions](https://github.com/anti-ltd/clink-actions) · [Fonts](https://github.com/anti-ltd/clink-fonts) · [Sounds](https://github.com/anti-ltd/clink-sounds)

## Included themes

This unofficial repository includes:

- **NuPhy Light**, a light Mechanical 3D theme with warm white caps and grey modifiers.
- **NuPhy Dark**, a dark Mechanical 3D theme with charcoal caps and dark modifiers.
- **Keychron Light**, a Mechanical 3D theme with soft grey caps, a silver-grey case, neutral light-grey modifiers, and coral-red accent keys.
- **Keychron Dark**, a charcoal Mechanical 3D theme with blue-grey modifiers and coral-red accent keys, inspired by the reference keyboard.
- **Akko Dark**, a navy Mechanical 3D theme with periwinkle caps, charcoal modifiers, and amber accent keys.
- **Akko Light**, a cream-cap Mechanical 3D theme with indigo modifiers and amber accent keys.

The NuPhy themes preserve Clink's debug palettes, including the teal plane toggle,
red Return, yellow spacebar, visible mechanical edges, and active/pressed key colours.
The Keychron themes use softly rounded sculpted caps, a spacebar matching the letter keys,
and a coral-red Return. The red plane toggle echoes the reference keyboard's Escape key;
active modifiers and the backspace press use the same accent.
The Akko themes use Canvas per-key paint: an amber plane toggle and Return echo the
reference board's Escape and Enter caps, the globe key takes the arrow cluster's amber
glyph on a dark cap, and 5–8 are painted dark to quote the board's function-row banding.
These themes are not affiliated with or endorsed by NuPhy, Keychron, or Akko.

The complete collection is published under [`Themes/`](Themes). The generated [`manifest.json`](manifest.json) describes every release asset.

## Make your first theme

You do not need to build Clink or write a manifest.

1. Fork this repository.
2. In Clink, make a theme and choose **Export** from the theme menu. This gives you a `.clinktheme` file.
3. Put the file in [`Themes/`](Themes), for example `Themes/my-theme.clinktheme`.
4. Open the file in a text editor. Give it a permanent lowercase `id` and a clear visible `name`.
5. Do not include `backgroundImageID` or `keyImageID`. Repository themes can contain colours, gradients, materials, and fonts, but not image files.
6. Run these commands:

   ```sh
   python3 tools/build-manifest.py
   python3 -m json.tool manifest.json >/dev/null
   ```

7. Push to `main`. GitHub Actions publishes a versioned release and marks it as the latest release.

## Add your repository to Clink

Open **General → Repositories** in Clink and add `owner/repository`, for example:

```text
anti-ltd/clink-themes-unofficial
```

Then open **Customize → Look**, choose your repository's chip, and download a theme. Downloaded themes remain available offline. They stay read-only, but anyone can make an editable copy.

## Make a theme with an AI agent

This repository includes [`PROMPT.md`](PROMPT.md), a ready-to-use brief for an AI coding agent. Fork the repository, open the fork in your agent, and say:

```text
Read PROMPT.md and create a [describe the visual direction] theme.
```

The prompt tells the agent which existing themes to inspect, which fields are safe to use, and how to regenerate the manifest. Review the resulting JSON and import it into Clink before publishing.

## What Clink verifies

Clink accepts only public HTTPS GitHub release manifests. Each theme must come from that repository's release, be a `.clinktheme` JSON file no larger than 128 KB, and match the SHA-256 hash and byte count in the manifest.

Clink downloads each file into a temporary directory, verifies its checksum and safe data-only structure, and only then installs it. Themes cannot contain photos or executable code.

Adding a repository is a trust decision. Only add repositories whose release contents you trust.

## Publishing is automatic

Keep `Themes/`, `tools/`, `tests/`, and `.github/workflows/` in your fork. Add or update a theme, regenerate the manifest, and push to `main`. GitHub Actions runs the manifest tests, builds the manifest, and publishes a versioned release so Clink can download the themes.

Release tags are derived from the theme files' contents. Each manifest points to
the exact version it describes; published assets and previous releases are kept.
This prevents cached previews or manifests from downloading replacement files
with different checksums. Clink still discovers updates through GitHub's
`releases/latest/download/manifest.json` address. Do not delete older releases,
including the original `latest` tag, while clients may still have their manifests.

Local manifest builds default to `anti-ltd/clink-themes-unofficial`. For a fork, set `GITHUB_REPOSITORY=owner/repository` when running the builder. GitHub Actions uses the actual repository name automatically.
