# Validation boundary

Existing OpenAI-compatible image provider via loopback bridge; Matrix delivery/encryption pending

# baibot reuse recipe

1. Run the bridge on the bot's host. For containers, `127.0.0.1` points to the container itself; use a co-located network setup or a separately secured reachable deployment instead of exposing an unauthenticated bridge.
2. In baibot create an `openai-compatible` agent and apply `openai-compatible-images.yml` as its image-generation configuration. Replace the placeholder with the separate bridge token, not the ToAPIs generation Key. Assign it only as the image-generation handler; keep existing text and voice providers.
3. Ask for the community-robot illustration. The inspected Rust controller posts `/images/generations` with `response_format=b64_json`; the bridge polls ToAPIs and returns actual PNG bytes. Set `style` and `quality` to null because the original DALL-E defaults do not match these model presets.
4. Change `model_id` to an exact model from the case table to compare the same prompt. Keep one output and 1024×1024.

The live JSON/base64 request boundary and PNG output were checked. The Rust bot, Matrix room delivery, encrypted-room permissions and image-editing path were not run. No native video generation route was found in the inspected provider contract, so video is not proposed for baibot. Its TTS/STT are separate upstream capabilities and are not ToAPIs capabilities established by this guide.



## Common checks

- Completed: three original image files, matching prompt/jobs, actual dimensions and PNG signatures; Key-scoped rate lookup; durable submission state; unsupported parameter rejection.
- Completed where video is included: decoded MP4, first-frame input, actual duration, settled task fee and case USD/s.
- Pending: full upstream app UI/runtime, package installation matrix, canvas/Matrix/gallery interactions, editing/masks, cancellation and concurrent multi-user deployment.
- Missing billing is not zero cost. Model/time-window log batches are not individual task-settlement proof.
