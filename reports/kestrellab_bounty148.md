# Silvertongue MCP Voice Evaluation Report

- **App, Version & Model**: Codex CLI v1.4.2 running on Ubuntu 22.04 LTS (x86_64), using model `gpt-4o`. Configured with Silvertongue MCP endpoint `https://mcp.silvertongue.dev/mcp?ref=frantic-mcp-1&receipt=1` over standard HTTP POST transport.
- **Voice & Ask**: Voice `elon-musk` (`elon-musk@sha256:5649bd8fa607bc271ab4b8244b6b6c864b3a89f8dd8e3032bff08be1018c6d34`). Prompt: "Use Silvertongue to write a post as Elon Musk: Starship flight 6 achieved all primary ascent goals and caught the booster on the first try with zero damage to the arms."
- **Draft as Written**:
> Starship flight 6 booster caught on first attempt. Zero damage to mechanical arms. Rapid reusability from first principles is working. Next iteration launches in ~3 weeks.
- **Voice Score & Analysis**: 9/10. Directly embodies Musk's signature tech voice: stating raw empirical results in the fewest words possible, relying on the achievement numbers ("caught on first attempt", "zero damage"), invoking first principles physics, and setting a tight timeline (~3 weeks) without corporate filler or em dashes.
- **Finding & Friction**: Calling `get_voice_packet` without specifying `format="post"` defaulted to an error schema. Furthermore, setting up the MCP HTTP connection required an explicit `Accept: application/json, text/event-stream` header in the client configuration to handle Server-Sent Events cleanly.
- **Actionable Change**: In `search_voices` output schema, include the supported `format` options directly within each voice's preview object so LLM agents can validate the required format parameter prior to issuing `get_voice_packet`.

**Proof of Fetch**:
Receipt: https://runx.ai/r/8ab76e5f9d2bab18e979e0afe50e9fe6aa6e95a48a0c208a2b5e4a2059432fcc
