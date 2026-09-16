# DROPPED — candidates that failed live verification

**Rule: unverifiable from this machine = dropped.** No "reportedly free", no "docs say". Each entry shows the exact probe and why it failed. Re-test before re-adding — networks, policies, and endpoints change.

*All probes run 2026-09-16 (UTC) from a Linux VM via curl/python. No browser, no signups performed.*

## Key-walled inference (401/403 without signup — free tier exists behind a free account)

| Candidate | Region | Probe | Result | Why dropped |
|---|---|---|---|---|
| DeepSeek API | CN | `GET api.deepseek.com/v1/models` (no key) | 401 | needs platform signup + key |
| Qwen / DashScope | CN | `GET dashscope.aliyuncs.com/compatible-mode/v1/models` | 401 | needs Alibaba Cloud signup + key |
| Moonshot / Kimi | CN | `GET api.moonshot.cn/v1/models` | 401 | needs signup + key |
| Zhipu GLM | CN | `GET open.bigmodel.cn/api/paas/v4/models` | 401 | needs signup + key |
| Mistral | EU | `GET api.mistral.ai/v1/models` | 401 | needs signup (+phone verify) + key |
| Aleph Alpha | EU | `GET api.aleph-alpha.com/models` | 401 | needs signup + key |
| Cohere | CA | `GET api.cohere.com/v1/models` | 401 | needs signup + key |
| Groq | US | `GET api.groq.com/openai/v1/models` | 401 | needs signup + key |
| Cerebras | US | `GET api.cerebras.ai/v1/models` | 403 | needs signup + key |
| SambaNova | US | `GET api.sambanova.ai/v1/models` → 200 (catalog public) | inference needs key | models list is public; inference requires signup + key |
| Together AI | US | `GET api.together.xyz/v1/models` | 401 | needs signup + key |
| Fireworks | US | `GET api.fireworks.ai/inference/v1/models` | 401 | needs signup + key |
| OpenRouter inference | US | catalog `GET /api/v1/models` → 200 (verified, in registry) | inference needs key | `:free` models need a free signup key — one signup away |
| Hugging Face Inference Providers | global | no-auth probe to router | auth-walled; stored token 401 | needs valid HF token (reconnect pending) |
| Hetzner Inference API | EU | `GET inference.hetzner.com/api/v1/models` (no token) | 401 | **needs free Hetzner account + API token** — free while experimental (500M in / 5M out tokens/day, Qwen3.6-35B, OpenAI-compatible). Highest-value signup on this list. |
| GitHub Models | US | `POST models.github.ai/inference/chat/completions` with PAT | **410 Gone** | endpoint retired |

## Dead / unreachable / changed

| Candidate | Probe | Result | Why dropped |
|---|---|---|---|
| DuckDuckGo AI Chat | `GET duckduckgo.com/duckchat/v1/status` | anti-bot JS challenge (`x-vqd-hash-1`), no `vqd-4` token issued | needs browser JS execution — not curl-usable |
| Puter.js | `POST api.puter.com/v2/ai/chat` and `/v2/drivers/call` | 404 both | API requires puter.com session auth |
| ToolPipe | `GET toolpipe.dev/uuid/generate` | connection closed / 000 | host unreachable from this VM |
| Argos Translate | `POST translate.argosopentech.com/translate` | connection closed / 000 | host unreachable from this VM |
| StreamElements TTS | `GET api.streamelements.com/kappa/v2/speech?voice=Brian&text=...` | 401 "No API key was found" | now requires API key |
| WorldTimeAPI | `GET worldtimeapi.org/api/timezone/Etc/UTC` | connection closed / 000 | host dead |
| RestCountries v3.1 | `GET restcountries.com/v3.1/name/france` | deprecated → "migrate to v5" | v3.1 retired; v5 path not verified |
| Jina Search Grounding | `GET s.jina.ai/?q=...` | 401 AuthenticationRequiredError | now requires API key (Reader still keyless — in registry) |
| x402 Bazaar (`x402.org/bazaar`) | `GET` → 301 → 404 "Page not found" | path gone; no bazaar link on x402.org homepage | moved or removed — do not cite old URL |

## Signup-gated (not probed — require accounts we can't create from here)

- **Cloud/inference:** Google AI Studio/Gemini, NVIDIA NIM, Cloudflare Workers AI — free tiers exist, all need signup + key.
- **Hosting/compute:** Cloudflare Pages/Workers, Vercel, Netlify, Deno Deploy, Fly.io, Oracle Always-Free, GCP free tier, Replit, Glitch — all need account signup.
- **Storage/data:** Supabase, Turso, Neon, Upstash, Cloudflare R2/KV — all need account signup.
- **Payments:** Stripe test mode (needs API key); Base Sepolia faucets (Alchemy/Coinbase/Google — need account signup or browser).
- **Search:** Brave Search, Tavily — need API keys.
- **Research compute grants:** EuroHPC/AI Factories, AWS/GCP research credits — require applications, not directly usable.

## Re-test policy

Before re-adding anything: re-run the exact probe, get a 200 with real data, record the UTC timestamp. A signup completed by the owner (e.g. Hetzner, OpenRouter, Groq) promotes the candidate from this file into the registry with a live receipt.

## Deep keyless sweep additions (2026-09-16 ~22:00 UTC)

| Candidate | Probe | Result | Why dropped |
|---|---|---|---|
| ApiAirforce | `POST api.airforce/v1/chat/completions` (no key) ×2 | **401 "Missing Authorization"** (`auth_required`) both times; `/v1/models` → 200 (612 models, catalog public) | chat requires auth — keyless claim false |
| Kilo AI Gateway | `POST api.kilo.ai/api/gateway/chat/completions` (no key, models `Hy3`, `kilo-auto-free`) ×2 | **401 PAID_MODEL_AUTH_REQUIRED** "You need to sign in to use this model" | "anonymous free" docs claim false — sign-in required |
| Blackbox AI | `POST www.blackbox.ai/api/chat` → 404 HTML; `GET /api/models` → 404 | no API surface | endpoint dead/removed |
| KeylessAI worker | `POST keylessai.thryx.workers.dev/v1/chat/completions` ×2; `/health` → 000 | connection closed / empty reply | aggregator down (its upstreams Pollinations + ApiAirforce probed directly) |
| Pollinations new API (`gen.pollinations.ai/v1`) | `GET /v1/models` → 200 (372 models); `POST /v1/chat/completions` ×3 (qwen/deepseek/llama) | **401 "A valid API key is required"** | only the LEGACY `text.pollinations.ai/openai` endpoint is anonymous (1 model: `openai-fast`) |
| OVHcloud chat completions | `POST /v1/chat/completions` ×5 (Qwen3-32B, Llama-3.3-70B, Mistral-7B, gpt-oss-20b; exact catalog IDs) | **429** every time (`x-ratelimit-remaining-minute: 0`) | anonymous tier documented (2 RPM/IP/model) but persistently throttled from this shared egress IP; embeddings + STT on same host serve fine — retry chat from a different IP |
| OVHcloud TTS (`nvr-tts-en-us`) | `POST /v1/audio/speech` ×2 | 400 then 404 "unknown endpoint" | endpoint path/params unverified — use Google Translate TTS instead |
| HuggingChat | `GET huggingface.co/chat/` | 200 HTML, no anonymous inference surface | login required for inference → see NOT-KEYLESS.md |
| HF Spaces (gradio) | 2 llama chat spaces: `chuanli11/...uncensored` → 503 "space is in error"; `srgtuszy/llama-3.2-chatbot` → 502 | spaces dead | old demo spaces unmaintained; route is low-yield |
| DuckDuckGo AI Chat | retry with browser headers: `GET /duckchat/v1/status` → 200 but no `vqd-4` token | anti-bot stands | 2nd failed probe — stays dropped |
| Puter.js | `PUT /v2/drivers/call` (documented shape) → read timeout | 2nd failed probe (was 404) | stays dropped |
| TextSynth | `GET api.textsynth.com/v1/engines` → 404 | key required per docs | → NOT-KEYLESS.md |
