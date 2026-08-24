# Config Generator

A single-file, offline browser tool that turns a Jinja template (and optional variable definitions) into standardized Cisco IOS switch configurations. Fill out a generated form, and the tool produces a clean config ready to paste into a terminal.

## Features

- **Jinja2 templating** with the familiar Ansible subset: variable substitution, defaults, filters (`upper`, `lower`, `trim`, `join`), and `{% if %}/{% else %}` conditional blocks.
- **Form generated automatically** from the template's variables, or from an optional vars file where each field defines its own help text, placeholder, default, and grouping.
- **Input validation** including regex patterns with custom error text, integer-only fields, and required vs. optional fields, plus template syntax checking that flags malformed Jinja before it reaches a device.
- **Dropdowns and linked field groups**, where filling one field in a group makes the rest required.
- **Copyable sections** for pasting long configs in stages: section markers split the preview into individually copyable cards with a copy-and-advance workflow, and critical sections can be flagged with red headers.
- **Manual edits at the template level**: tweak any section or the full config in place, and `{{ variable }}` entries keep working inside the edited text as the form changes.
- **Inline compliance badges** (`!STIG:`, `!CIS:`, or any all-caps keyword), color-coded per keyword. Badges and template comments are stripped when the config is copied or saved.
- **Live preview** with IOS syntax highlighting. Click a variable in the preview to jump to its form field, or click a field label to find every place it appears in the config.
- **Save and load sessions** to pick up where you left off, plus saving configs and templates to disk.
- **Fully offline and self-contained.** One HTML file, no install, no build step, no network.

## Security

Config data lives only in memory while the tab is open. No configurations or form values are written to browser storage, and they are gone once the tab is closed. Anything you want to keep must be explicitly saved to disk.

## Usage

Open `config-generator.html`, load a template (and optionally a vars file), fill out the form, then copy or save the result. Files can also be dragged and dropped onto the form panel. The built-in guide documents the full template and vars file syntax, including every supported key.

Chromium-based browsers (Edge, Chrome) use the File System Access API, so open and save dialogs reopen in the last folder used. Browsers without that API fall back to standard download and file-input behavior.
