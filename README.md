# Config Generator

A single-file, offline browser tool that turns a Jinja template (and optional variable definitions) into standardized network switch configurations. Fill out a generated form, and the tool produces a clean config ready to paste into a terminal. Built and device-tested for Cisco IOS XE, with beta support for NX-OS, Arista EOS, and Juniper Junos.

## Features

- **Jinja2 templating** with the familiar Ansible subset: variable substitution, defaults, filters (`upper`, `lower`, `trim`, `join`), and `{% if %}/{% else %}` conditional blocks.
- **Form generated automatically** from the template's variables, or from an optional vars file where each field defines its own help text, placeholder, default, and grouping.
- **Input validation** including regex patterns with custom error text, integer-only fields, and required vs. optional fields.
- **Dropdowns and linked field groups**, where filling one field in a group makes the rest required.
- **Paste warnings** on the rendered output: `?` (opens CLI help), tab (triggers completion), non-ASCII characters, over-long descriptions, unclosed banners, and template syntax that failed to render. Each one marks its line, underlines the exact spot, and is listed on the section header with click-to-jump. A literal Ctrl-V before `?` or tab is honored as the IOS editor escape. Copy and save still work; the warning count rides along on the toast.
- **Template and vars file checks**: unmatched `{% if %}`/`{% endif %}`, unsupported tags, split expressions; unknown keys, bad defaults, duplicate names, orphaned groups, and more. Hover the badge under each file for the list.
- **Copyable sections** for pasting long configs in stages: section markers split the preview into individually copyable cards with a copy-and-advance workflow, and critical sections can be flagged with red headers.
- **Manual edits at the template level**: tweak any section or the full config in an editor with keyword and Jinja highlighting, Tab indent, and the same paste warnings live as you type. `{{ variable }}` entries keep working inside the edited text as the form changes.
- **Inline compliance badges** (`!STIG:`, `!CIS:`, or any all-caps keyword), color-coded per keyword. Badges and template comments are stripped when the config is copied or saved.
- **Live preview** with syntax highlighting. Click a variable in the preview to jump to its form field, or click a field label to find every place it appears in the config.
- **Multiple platforms.** Comment syntax, section markers, banner grammar, description limits, and keyword colors follow the selected platform; switch from the badge in the preview title, or let the tool detect the platform from a loaded template. Sessions remember the choice.
- **Create a template from scratch** when none is loaded, or **save and load sessions** to pick up where you left off, plus saving configs and templates to disk.
- **Fully offline and self-contained.** One HTML file, no install, no build step, no network.

## Platforms

| Platform | Comment | Section marker | Status |
| --- | --- | --- | --- |
| Cisco IOS / IOS XE | `!` | `!!! Name` | Device-tested |
| Cisco NX-OS | `!` | `!!! Name` | Beta |
| Arista EOS | `!` | `!!! Name` | Beta |
| Juniper Junos | `#` | `### Name` | Beta |

Beta platforms are parsed and linted from the vendor grammars but have not been verified against hardware. Verify output on a device before relying on it. Everything platform-specific lives in the `DIALECTS` table near the top of the script; adding a platform is adding an entry.

## Configuration

A short block of constants at the top of the script tailors the tool for a site:

| Constant | Default | Effect |
| --- | --- | --- |
| `LINT_PASTE_WARNINGS` | `true` | Paste warnings in the preview, editors, section headers, and copy/save toasts |
| `LINT_TEMPLATE` | `true` | Template syntax badge |
| `LINT_VARS_FILE` | `true` | Advisory vars file checks (parse errors always show) |
| `DIALECT_NAME` | `"ios"` | Platform at startup: `ios`, `nxos`, `eos`, `junos` |
| `DIALECT_AUTODETECT` | `true` | Switch platform on template load when the text makes it clear |
| `EDITOR_TAB_SIZE` | `4` | Spaces inserted by Tab in editors; `0` restores focus navigation |
| `EDITOR_HIGHLIGHTING` | `true` | Keyword and Jinja coloring in editors |

## Security

Config data lives only in memory while the tab is open. No configurations, form values, or platform selections are written to browser storage, and they are gone once the tab is closed. Anything you want to keep must be explicitly saved to disk.

## Usage

Open `config-generator.html`, load a template (and optionally a vars file) or create a new template, fill out the form, then copy or save the result. Files can also be dragged and dropped onto the form panel. The built-in guide documents the full template and vars file syntax, including every supported key, with examples in the selected platform's syntax.

Chromium-based browsers (Edge, Chrome) use the File System Access API, so open and save dialogs reopen in the last folder used and a saved template's chosen filename is adopted by the tool. Browsers without that API fall back to standard download and file-input behavior.
