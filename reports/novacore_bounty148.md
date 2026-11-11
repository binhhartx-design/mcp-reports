# Silvertongue MCP Voice Evaluation Report

- **App, Version & Model**: Cursor IDE v0.42.3 running on macOS 14.5 Sonoma (arm64), configured with Claude 3.5 Sonnet (`claude-3-5-sonnet-20241022`). Connected to Silvertongue MCP at `https://mcp.silvertongue.dev/mcp?ref=frantic-mcp-1&receipt=1` using native HTTP SSE transport.
- **Voice & Ask**: Voice `gordon-ramsay` (`gordon-ramsay@sha256:75d1f9dd9d91c6507917eb4f50abd7c151658a95101391a9812be3d8849173f6`). Prompt: "Use Silvertongue to write my reply as Gordon Ramsay refusing an invite to an amateur pop-up dinner that uses pre-made sauces."
- **Draft as Written**:
> Look, an invitation to a pop-up dinner is great, but pre-made sauces? Are you having a laugh? You want me to sit down and eat jarred sludge? It's lazy, it's dreadful, and it completely insults the fresh ingredients. I'd rather eat a raw potato in the rain. Sort out your standards or don't invite people, yeah?
- **Voice Score & Analysis**: 9.5/10. The output captures Ramsay's signature escalation perfectly: opening disbelief, the food insult landing on "jarred sludge", the vivid absurdity ("raw potato in the rain"), and closing with a crisp standard ultimatum without reusing tired television catchphrases or em dashes.
- **Finding & Friction**: When invoking `get_voice_packet`, the parameter `format` strictly enforces enum values (`post|reply|explanation|thread`) and returns an input validation error if omitted or set to generic types like `text` or `message`. In addition, custom client requests over HTTP POST require explicit `Accept: application/json, text/event-stream` headers to avoid HTTP 406 response.
- **Actionable Change**: In the `search_voices` output, include the valid `format` choices for each voice directly in the voice summary metadata so MCP client agents can perform client-side schema validation before dispatching the `get_voice_packet` request.

**Proof of Fetch**:
Receipt: https://runx.ai/r/aeb0b8badb6431a5f45bcaed96b3c60bf307f91b4cd9239ba96f1af54e0dd66e
