# Config Generator

A single-file, offline browser tool that turns a Jinja template and an optional vars file into a device configuration through a generated form. Built and device-tested for Cisco IOS XE; NX-OS, Arista EOS, and Juniper Junos are supported but untested.

## Features

- Jinja2 subset compatible with Ansible: `{{ VAR }}`, `default`, `upper`, `lower`, `trim`, `join`, and `{% if %}`, `{% if not %}` and `{% else %}` blocks.
- Form generated from the template's variables, or from a vars file that adds hints, placeholders, defaults, dropdowns, built-in checks for IPv4 addresses, masks, wildcards, VLANs and hostnames, number ranges, regex validation, linked field groups, and one-way requirements.
- Live highlighted preview: click a variable to jump to its field, or a field label to find it in the config; code a condition leaves out stays visible as comments.
- Copyable sections: `!!! Name` markers split the preview into cards with a copy-and-advance workflow.
- Manual edits at the template level in a highlighted editor; variables keep working inside edited text.
- Paste warnings for `?` and tab (unless escaped with Ctrl-V), non-ASCII, over-long descriptions, unclosed banners, and unrendered template syntax, marked in place and listed on the section header.
- Template and vars file checks: unmatched tags, unsupported syntax, unknown keys, bad defaults, duplicates, unanchored regexes, and categories split across the file.
- Inline badges: `!STIG: V-1234` or any all-caps keyword renders a colored pill; badges and template comments are stripped from output.
- Sessions save the whole workspace as one JSON file, except values of secret fields, which stay masked on screen too; nothing is written to browser storage, so nothing else survives closing the tab.
- The platform badge in the preview title switches the platform, and loading a template picks it automatically when the syntax is unambiguous; Generic turns every platform rule off as a fallback.

## Platforms

- Cisco IOS XE (device-tested)
- Cisco NX-OS (untested)
- Arista EOS (untested)
- Juniper Junos (untested)
- Generic: no platform rules; only template syntax, section markers and badges are removed, lines keep their indentation, and `!` or `#` is read from the template's markers

## Configuration

Constants at the top of the script:

| Constant | Default | Effect |
| --- | --- | --- |
| `STRIP_COMMENTS` | `true` | Drop comment lines and inline comments from output |
| `STRIP_BADGES` | `true` | Render `!KEYWORD:` badges and drop them from output; off leaves them as comment text |
| `STRIP_INDENT` | `true` | Remove leading indentation from output lines |
| `FREEFORM_COMMANDS` | `[]` | Extra commands whose mid-line comment character is data |
| `OUTPUT_EXTENSION` | `".config"` | Extension for saved config and template files |
| `OUTPUT_CRLF` | `true` | Windows line endings in saved config and template files |
| `COPY_TRAILING_NEWLINE` | `true` | Copied text ends with a newline so the last line executes |
| `FILENAME_VAR` | `"HOSTNAME"` | Form variable (any casing) that names saved files |
| `TEMPLATE_EXTENSIONS` | `".config,.txt,..."` | Template picker filter |
| `SAVE_TEMPLATE_HEADER` | `true` | Prepend the syntax header when saving a template |
| `AUTO_DETECT_VARS` | `true` | Keep the form in sync with the template; off shows a lightning button to detect manually |
| `LINT_PASTE_WARNINGS` | `true` | Paste warnings in the preview, editors, headers, and toasts |
| `LINT_NON_ASCII` | `true` | Flag non-ASCII characters; off for sites with umlauts in banners |
| `LINT_TEMPLATE` | `true` | Template syntax badge |
| `LINT_VARS_FILE` | `true` | Advisory vars file checks (parse errors always show) |
| `DIALECT_NAME` | `"ios"` | Startup platform: `ios`, `nxos`, `eos`, `junos`, `generic` |
| `DIALECT_AUTODETECT` | `true` | Switch platform on template load when the text makes it clear |
| `EDITOR_TAB_SIZE` | `4` | Spaces inserted by Tab in editors; `0` restores focus navigation |
| `EDITOR_HIGHLIGHTING` | `true` | Keyword and Jinja coloring in editors |

## Usage

Open `config-generator.html`, load or create a template, fill out the form, then copy or save. Files can be dropped anywhere in the window. The built-in guide covers template and vars file syntax.

Chromium browsers use the File System Access API, so dialogs reopen in the last folder and a saved template's filename is adopted. Other browsers fall back to downloads.
