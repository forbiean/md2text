# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-page Markdown-to-plain-text converter tool. Pure frontend, no build step, no dependencies — just one `index.html` file.

## Architecture

Everything lives in `index.html`:

- **CSS**: Embedded `<style>` block. Dark theme using CSS variables (`--bg-deep`, `--accent`, etc.). JetBrains Mono + Noto Sans SC fonts loaded from Google Fonts.
- **HTML**: Two-pane layout (left: Markdown textarea input, right: read-only plain text output). Toolbar buttons per pane (copy/download). Footer with "load example" and "clear" buttons.
- **JS**: Embedded `<script>` block containing:
  - `md2txt()` — main converter, processes line-by-line: headings, blockquotes, lists (nested), code blocks, tables, horizontal rules, then delegates inline syntax to `inlineConvert()`.
  - `inlineConvert()` — strips/converts inline Markdown (bold, italic, strikethrough, links, images, inline code, HTML tags).
  - `formatTable()` — renders Markdown tables as aligned plain-text with box-drawing characters. Uses `getDisplayWidth()` for CJK-aware column alignment.
  - Scroll sync between the two textareas (proportional scrollTop).
  - UI helpers: `copyText()`, `download()`, `loadExample()`, `clearAll()`, toast notifications.

## Development

Open `index.html` directly in a browser. No server or build tools needed. Edit and refresh.

## Key Conventions

- Chinese (zh-CN) UI language.
- Markdown conversion targets readable plain text, not raw strip — e.g., `#` headings become uppercased with underline decorations, lists use `•◦▪▸` bullets, blockquotes use `│` prefix, tables use box-drawing characters.
