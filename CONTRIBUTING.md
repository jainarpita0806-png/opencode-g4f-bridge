# Contributing to OpenCode G4F Bridge

Thank you for your interest in contributing to the OpenCode G4F Bridge! 

## How to Contribute

### 1. Reporting Bugs
If you find that a specific AI proxy network's SSE stream is crashing OpenCode, please open an issue with the raw chunks (use `-t` or capture the raw terminal output) so we can add a sanitization rule for it.

### 2. Suggesting Enhancements
We are always looking to support more proxy networks (beyond G4F and EAON). If you know of a reliable proxy that provides an OpenAI-compatible `/v1/models` endpoint, feel free to suggest it or open a PR!

### 3. Pull Requests
1. Fork the repo and create your branch from `main`.
2. If you've added code that changes the config generation, make sure you test it with OpenCode's visual UI limits (max 15 items per catalog) and ensure pagination still works.
3. Keep the code clean and strictly avoid hardcoding any API keys or secrets in the repository.
4. Issue a pull request describing your changes.

## Code Style
- Keep the `smart_bridge.py` script as a lightweight, single-file server. Do not add bloated dependencies unless absolutely necessary.
