# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

clipboard2markdown is a browser-based tool that converts richly formatted text or HTML to Markdown. Users paste content and it's instantly converted using the to-markdown library.

## Running the Application

Open `index.html` directly in a browser. No build step or server required.

## Architecture

This is a client-side only application with no dependencies or build system.

**Core files:**
- `index.html` - Main page with paste input area and output textarea
- `clipboard2markdown.js` - Application logic: handles paste events, applies Pandoc-style converters, and escapes smart punctuation
- `to-markdown.js` - Bundled third-party library (dom christie's to-markdown) that does the HTML-to-Markdown conversion

**Conversion flow:**
1. User pastes content → captured by keydown listener in contenteditable `#pastebin` div
2. HTML content passed to `toMarkdown()` with custom Pandoc converters and GFM enabled
3. Smart punctuation escaped (curly quotes → straight quotes, em-dashes → `---`, etc.)
4. Result inserted into `#output` textarea

**Custom converters in clipboard2markdown.js:**
- Setext-style headers (h1/h2 with underlines)
- Superscript/subscript (`^text^` / `~text~`)
- Auto-linking for URLs matching their text content
- Pandoc-style list item formatting
