# Why Did My Model Fail The Live Test?

If you ran the bridge with the `-t` flag and a model failed the test, it's not a bug in the bridge! 

The `-t` flag runs a **Strict OpenCode Compatibility Stress Test**. We intentionally design this test to crash weak proxy models so they don't break your OpenCode UI later. 

Here are the exact reasons why a model might fail the test:

## 1. The "Content Too Large" (413) Error
OpenCode relies on sending massive context payloads (often 20,000 to 40,000+ tokens) to the AI model so it can read all your project files at once. 

Many free proxy networks (like Groq via G4F) have strict **8,000 Tokens Per Minute (TPM)** limits. If you try to use one of these models in OpenCode, it will instantly crash. 
**How we test this:** Our test injects a massive 15,000+ token dummy string into the system prompt. If the model throws a `413 Content Too Large` error, we automatically fail it and block it from your UI.

## 2. The "Tools Not Supported" (400) Error
OpenCode relies heavily on OpenAI's `tools` array (Function Calling) to execute terminal commands, read files, and write code. 

If an upstream proxy model does not support tool calling (or if it crashes when it sees strict JSON schema parameters), OpenCode will completely freeze or throw a `400 Bad Request` error.
**How we test this:** Our test injects a strictly formatted dummy `tools` array into the payload. If the model rejects it, we automatically fail it.

## 3. Provider Timeout / Dead Proxy (502 / 504)
Free proxy networks are highly volatile. Sometimes, the server hosting `gpt-5` or `claude-3` simply crashes or gets overloaded, leaving your connection hanging indefinitely.
**How we test this:** Our bridge gives the model a strict **25-second timeout** to accept the connection and respond. If the proxy server is dead and doesn't respond in time, we automatically drop it so you only get healthy models in your configuration.
