# Config Generator

A single-file, offline browser tool that turns a template and a variable definition file into standardized Cisco IOS switch configurations. Fill out a generated form, and the tool produces a clean, validated config ready to paste into a terminal.

## Features

- **Jinja2 templating** with the familiar Ansible subset: variable substitution, defaults, filters (`upper`, `lower`, `trim`, `join`), and `{% if %}/{% else %}` conditional blocks.
- **Form generated from a vars file**, where each field defines its own help text, placeholder, default, and layout.
- **Input validation** including regex patterns with custom error text, integer-only fields, and required vs. optional fields.
- **Dropdowns and field groups**, including all-or-nothing linked groups where filling one field makes the rest required.
- **Section breaks and headers** for organizing long configs, with optional red highlighting for critical sections.
- **Inline compliance badges** (`!STIG:`, `!CIS:`, or any all-caps keyword), color-coded per keyword and automatically stripped when the config is copied.
- **Live preview** of the rendered config as the form is filled.
- **Save and load sessions** to pick up where you left off, plus saving configs and templates to disk.
- **Fully offline and self-contained.** One HTML file, no install, no build step, no network.

## Security

Config data lives only in memory while the tab is open. No configurations or form values are written to browser storage, and they are gone once the tab is closed. Anything you want to keep must be explicitly saved to disk.

## Usage

Open `config-generator.html`, load a template and a vars file, fill out the form, then copy or save the result. The included example files cover the full template and variable syntax.
