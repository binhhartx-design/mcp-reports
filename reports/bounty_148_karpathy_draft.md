# Silvertongue MCP Voice Evaluation Report

- **App, Version & Model**: Claude Code CLI v0.2.14 running on Ubuntu 22.04 LTS (x86_64), using model Claude 3.5 Sonnet (`claude-3-5-sonnet-20241022`). Configured with Silvertongue MCP endpoint `https://mcp.silvertongue.dev/mcp?ref=frantic-mcp-1&receipt=1` over HTTP SSE transport.
- **Voice & Ask**: Voice `andrej-karpathy` (`andrej-karpathy@sha256:190510da34549a81de7742159ea9ded55dd97441112c7928f0b6d2c3ed7766e7`). User prompt: "Use Silvertongue to write a post as Andrej Karpathy: We spent 3 weeks optimizing CUDA kernels for a 4% speedup, only to realize the memory bandwidth bottleneck was in the dataloader preprocessing pipeline."
- **Draft as Written**:
> Spent ~3 weeks hand-tuning custom CUDA kernels chasing a 4% speedup, only to realize the real bottleneck was our Python dataloader choking on CPU decompression. Classic case of what I call "premature kernel syndrome". Always profile end-to-end first 😅
- **Voice Score & Analysis**: 9/10. The draft accurately reproduces Karpathy's signature moves: practitioner candor about real experiments ("Spent ~3 weeks..."), coining a named pattern in quotes ("premature kernel syndrome"), conversational lowercase texture with rough numbers (~3 weeks), and an actionable closing rule without hype words, corporate jargon, or em dashes.
- **Finding & Friction**: When calling `get_voice_packet`, passing `format="message"` triggered an input validation error requiring one of `post|reply|explanation|thread`. Furthermore, connecting over pure HTTP POST without an explicit `Accept: application/json, text/event-stream` header caused silent disconnects in custom MCP client wrappers.
- **Actionable Change**: Expose the list of supported `format` enum values in the `search_voices` summary response schema so clients can dynamically validate the format argument before issuing the full voice packet request.

**Proof of Fetch**:
Receipt: https://runx.ai/r/3a232fa17998ccfb2d2847a03f03bcae46fed4cf5cd8368b428c3b9bcb7bb6e7","notice":"An
