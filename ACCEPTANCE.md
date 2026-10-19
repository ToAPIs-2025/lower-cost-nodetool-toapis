# Validation boundary

Loopback OpenAI-compatible bridge for existing custom image/video endpoints; app UI pending

# NodeTool reuse recipe

1. Run the bridge on the same host as self-hosted NodeTool. The generated API Key remains on the bridge server.
2. In Settings → Models & providers → OpenAI-compatible endpoints, add name `ToAPIs media bridge`, slug `toapis`, Base URL `http://127.0.0.1:8769/v1`, and your separate local `BRIDGE_TOKEN` as the endpoint key. Copy the image/video lists from `custom-provider-catalog.json`; this file documents the existing catalog shape, it is not a new import button.
3. For images select one of the three enabled models, PNG, one output and a 1K request. The bridge returns synchronous base64 after polling ToAPIs.
4. For image-to-video select `seedance-2-mini`, 4 seconds, 1280×720, no audio. The bridge handles OpenAI multipart `input_reference` / `seconds` / `size`, then `/videos/{id}` and `/videos/{id}/content`. The published live sample uses exactly this multipart/poll/download API boundary. Set the node timeout to at least 15 minutes.

The bridge requires a first-frame PNG. Text-to-video, image editing and chat/audio routes are disabled. The full NodeTool app UI/runtime was not launched. Cloud-profile NodeTool rejects loopback endpoints by design; this local recipe is for self-hosted use. Do not bypass its SSRF policy. A hosted HTTPS deployment or a maintainer-reviewed direct Provider is a separate integration task.

Keep the project's existing Atlas Cloud sponsor/referral entry unchanged. This is an optional independently maintained endpoint recipe, not a replacement sponsor or exclusivity claim.



## Common checks

- Completed: three original image files, matching prompt/jobs, actual dimensions and PNG signatures; Key-scoped rate lookup; durable submission state; unsupported parameter rejection.
- Completed where video is included: decoded MP4, first-frame input, actual duration, settled task fee and case USD/s.
- Pending: full upstream app UI/runtime, package installation matrix, canvas/Matrix/gallery interactions, editing/masks, cancellation and concurrent multi-user deployment.
- Missing billing is not zero cost. Model/time-window log batches are not individual task-settlement proof.
