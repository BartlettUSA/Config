# Gemini Code Assist Instructions

Always use context7 when I need code generation, setup or configuration steps, or library/API documentation. Automatically use the Context7 MCP tools to resolve library id and get library docs without me having to explicitly ask.

## Context7 MCP Tools

- `resolve-library-id` - Find the Context7 library ID for any package
- `get-library-docs` - Fetch current documentation for a library

## Usage

No need to say "use context7" - it will be invoked automatically for any code-related questions involving external libraries.

This ensures code examples use current APIs and avoid deprecated patterns.
