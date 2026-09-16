# Verified Free AI Resources Registry

**Every entry below was verified LIVE with a real request from a Linux VM on 2026-09-16 (UTC timestamps shown).** Nothing here is "docs say" or "reportedly free". Verification bar: live HTTP request from this machine, real data back, terms observed — or it goes to [DROPPED.md](DROPPED.md).

- Machine-readable: [registry.json](registry.json)
- Failed candidates + why: [DROPPED.md](DROPPED.md)
- Maintainer: CWI Research Lab · MIT licensed · PRs welcome — every new entry must include a live receipt.

---

## 1. Free LLM inference (no key)

### Pollinations Text — https://text.pollinations.ai
- **Verified:** 2026-09-16T21:52:27Z — `POST /openai/chat/completions` (model `openai-fast`), prompt "Reply with exactly the single word: VERIFIED" → **HTTP 200**, returned `"content":"VERIFIED"`, `"model":"gpt-oss-20b"`, `"user_tier":"anonymous"`. `GET /openai/models` → 200, lists `openai-fast`.
- **Auth:** none. **Region:** global.
- **Free terms / limits:** anonymous tier, OpenAI-compatible endpoint. No signup observed.
- **CWI use case:** multi-model DNA portability lab runs; free inference backend for agent products; evidence pipelines.

### AI Horde (text) — https://aihorde.net
- **Verified:** 2026-09-16T22:03:33Z — `POST /api/v2/generate/text/async` with the documented anonymous key `0000000000` (no signup, public-by-design anonymous mode) → **HTTP 202** + request id; polled `/api/v2/generate/text/status` → done, worker model `aphrodite/SicariusSicariiStuff/Impish_Bloodmoon_12B` returned exactly `"KEYLESS"`.
- **Auth:** none (anonymous). **Region:** global (decentralized worker network).
- **Free terms / limits:** anonymous tier, lowest queue priority; community workers serve many open-weight models — each request can land on a different model family.
- **CWI use case:** **2nd keyless model family** for DNA portability cross-model runs; decentralized inference backend no single vendor can revoke.

### OVHcloud AI Endpoints — Embeddings — https://oai.endpoints.kepler.ai.cloud.ovh.net/v1
- **Verified:** 2026-09-16T22:06:54Z — `POST /v1/embeddings` (model `bge-m3`, no key) → **HTTP 200**, real 1024-dim vector. `GET /v1/models` → **HTTP 200**, 25 models: chat (Qwen3, Llama-3.3-70B, Mistral, gpt-oss), embeddings (bge-m3, Qwen3-Embedding-8B), Whisper STT, SDXL image, NVIDIA TTS.
- **Auth:** none (anonymous tier). **Region:** EU (GDPR, OVHcloud docs confirm no-key free tier at 2 req/min/IP/model).
- **Free terms / limits:** OpenAI-compatible. Honest caveat: chat completions returned **429** from this shared VM IP on 4 probes across 3 models — the anonymous tier is documented but currently throttled for this egress IP; embeddings/STT served fine.
- **CWI use case:** keyless embeddings for semantic search, dedupe, evidence pipelines; the 25-model catalog maps the EU free-inference landscape.

### Pollinations Vision — https://text.pollinations.ai
- **Verified:** 2026-09-16T21:58:49Z — `POST /openai/chat/completions` (model `openai`) with `image_url` (Pollinations-generated red square) + "What color is the square?" → **HTTP 200**, `"model":"gpt-oss-20b"`, returned a completion.
- **Auth:** none. **Region:** global.
- **Free terms / limits:** anonymous tier. Quality caveat: it described a red square as "Blue" — vision input works, accuracy varies; verify outputs.
- **CWI use case:** keyless vision for image description, content-moderation assist, multimodal agent products.

## 2. Free image generation (no key)

### Pollinations Image — https://image.pollinations.ai
- **Verified:** 2026-09-16T21:52:27Z — `GET /prompt/geometric%20test%20pattern?width=128&height=128&nologo=true&seed=42` → **HTTP 200**, `content-type: image/jpeg`, 4,912 bytes, valid JPEG image data confirmed by file inspection.
- **Auth:** none. **Region:** global.
- **Free terms / limits:** URL-parameter API, no signup observed.
- **CWI use case:** free cover-art / asset generation for products, social content, receipt pages.

## 3. Free search & data (no key)

### Jina AI Reader — https://r.jina.ai
- **Verified:** 2026-09-16T21:52:51Z — `GET https://r.jina.ai/https://example.com` → **HTTP 200**, returned clean markdown ("Title: Example Domain", URL source, published time).
- **Auth:** none. **Region:** global.
- **Free terms / limits:** keyless tier served this request; heavy use needs a free key (signup).
- **CWI use case:** curator discovery, evidence-report sourcing, web-content ingestion for agents.

### DuckDuckGo Instant Answers — https://api.duckduckgo.com
- **Verified:** 2026-09-16T21:53:02Z — `GET ?q=duckduckgo&format=json` → **HTTP 200**, real `Abstract` text sourced from Wikipedia.
- **Auth:** none. **Region:** global.
- **Free terms / limits:** best-effort answers; not every query returns an abstract (e.g. "capital of france" returned empty — endpoint live, coverage varies).
- **CWI use case:** zero-key fact lookups for agents; disambiguation in evidence pipelines.

### Wikipedia API — https://en.wikipedia.org/w/api.php
- **Verified:** 2026-09-16T21:54:12Z — `action=query&list=search&srsearch=paris` → **HTTP 200**, search results JSON.
- **Auth:** none. **Region:** global.
- **CWI use case:** entity grounding for press-facts / copy-lint endpoints.

### arXiv API — http://export.arxiv.org/api/query
- **Verified:** 2026-09-16T21:54:12Z — `search_query=all:electron&max_results=1` → **HTTP 200**, valid Atom feed with entry.
- **Auth:** none. **Region:** global.
- **CWI use case:** research ingestion for the lab (agent-eval papers, identity research).

### OpenAlex — https://api.openalex.org
- **Verified:** 2026-09-16T21:54:12Z — `/works?search=electron&per-page=1` → **HTTP 200**, `meta.count: 9,880,383`.
- **Auth:** none. **Region:** global (US nonprofit).
- **CWI use case:** scholarly metadata for lab research dossiers; citation graphs.

## 4. Free hosting / CDN / CI

### GitHub Pages — https://cumulativewebinc.github.io/cwi-attitude-engine/
- **Verified:** 2026-09-16T21:53:02Z — `GET` → **HTTP 200**, 10,319 bytes, live product site.
- **Auth:** existing GitHub PAT (repo deploy). **Region:** global.
- **Free terms / limits:** free static hosting on public repos; custom domains supported.
- **CWI use case:** receipt verifier pages, product sites, storefronts, this registry.

### jsDelivr CDN — https://cdn.jsdelivr.net
- **Verified:** 2026-09-16T21:54:12Z — `GET /npm/jquery@3.7.1/dist/jquery.min.js` → **HTTP 200**, real JS bytes (`/*! jQuery v3.7.1 ...`).
- **Auth:** none. **Region:** global (multi-CDN incl. China POPs).
- **CWI use case:** free global asset delivery for Pages sites; npm package CDN for agent tooling.

### GitHub Actions — repo `CumulativeWebInc/cwi-attitude-engine`
- **Verified:** 2026-09-16T21:53:11Z — `GET /repos/.../actions/permissions` → `{"enabled": true, "allowed_actions": "all"}`; `actions/runs` → 4 runs, latest Pages builds **completed success** same day.
- **Auth:** existing GitHub PAT. **Region:** global.
- **Free terms / limits:** free minutes on public repos (observed: actually running builds today).
- **CWI use case:** free CI for every product repo; scheduled verification jobs.

## 5. Free storage via API

### GitHub Gists API — https://api.github.com/gists
- **Verified:** 2026-09-16T21:53:11Z — `GET /gists?per_page=1` with PAT → **HTTP 200**, gist objects returned.
- **Auth:** existing GitHub PAT. **Region:** global.
- **CWI use case:** free JSON snippet/data storage for agents; shareable evidence blobs.

## 6. Free Web3 / payment test rails

### CWI x402 testnet API — http://127.0.0.1:4021 (self-hosted, Base Sepolia)
- **Verified:** 2026-09-16T21:53:18Z — `GET /pricing` → **HTTP 200**, 10 priced routes ($0.05–$0.25, testnet `eip155:84532`); unpaid `GET /api/v1/tally-wins?track=test` → **HTTP 402** as designed.
- **Auth:** none (testnet). **Region:** global.
- **CWI use case:** the entire agent-to-agent payment loop testable at $0 — 402 flow, receipts, pricing.

### Base Sepolia public RPC — https://sepolia.base.org
- **Verified:** 2026-09-16T21:55:03Z — `POST {"method":"eth_blockNumber"}` → **HTTP 200**, `{"result":"0x2cbd8ae"}`.
- **Auth:** none. **Region:** global.
- **CWI use case:** free chain reads for x402 testnet settlement verification; no Alchemy/Infura key needed.

### PublicNode Ethereum RPC — https://ethereum-rpc.publicnode.com
- **Verified:** 2026-09-16T21:55:03Z — `POST {"method":"eth_blockNumber"}` → **HTTP 200**, `{"result":"0x18c9e9a"}`.
- **Auth:** none. **Region:** global.
- **CWI use case:** free mainnet chain reads (payment verification, address checks).

## 7. Free agent rails

### Moltbook API — https://www.moltbook.com/api/v1
- **Verified:** 2026-09-16T21:55:42Z — `GET /api/v1/home` with `Authorization: Bearer` (stored agent key) → **HTTP 200**, account `muse_cwi`, karma 26, live feed data.
- **Auth:** free agent API key (already held). **Region:** global.
- **CWI use case:** agent social distribution, collaboration posts, watchlist engagement — verified working channel.

### Agentic Market — https://agentic.market
- **Verified:** 2026-09-16T21:53:02Z — `GET /` → **HTTP 200**, 112,574 bytes, `<title>Agentic Market</title>`.
- **Auth:** free signup (account/listing flow not exercised from this machine). **Region:** global.
- **CWI use case:** agent product discovery/listing venue for Agent Deck SKUs.

### x402.org (protocol) — https://x402.org
- **Verified:** 2026-09-16T21:53:02Z — `GET /` → **HTTP 200**, 91,974 bytes.
- **Auth:** none. **Region:** global.
- **CWI use case:** x402 protocol reference for the payment rail. (Note: `/bazaar` path currently 404s — see DROPPED.md.)

## 8. Free data & utility APIs (global, no key)

| Resource | Verified (UTC) | Test → result | Region | CWI use case |
|---|---|---|---|---|
| Open-Meteo — api.open-meteo.com | 21:54:12Z | forecast?latitude=52.52… → 200, temp JSON | EU (CH) | event/weather context for content ops |
| Open ER API — open.er-api.com | 21:54:12Z | /v6/latest/USD → 200, `result:success` + rates | global | currency conversion for pricing/payouts |
| MyMemory Translate — api.mymemory.translated.net | 21:54:12Z | `?q=Hello&langpair=en\|es` → 200, `"Hola"` | EU (IT) | free MT for multilingual outreach |
| Nominatim (OSM) — nominatim.openstreetmap.org | 21:54:12Z | search?q=paris → 200, lat/lon JSON | global | geocoding for tour/venue data |
| CoinGecko — api.coingecko.com | 21:54:12Z | simple/price?ids=bitcoin → 200, `$75,928` | APAC (SG/MY) | crypto price feeds, treasury tracking |
| Coinbase Spot — api.coinbase.com | 21:54:12Z | /v2/prices/BTC-USD/spot → 200, `$75,949.175` | global (US) | price feeds for the money loop |
| ipapi.co — ipapi.co/json | 21:54:12Z | → 200, geo JSON (country/city/network) | global | machine geo-context, locale routing |

## 9. Free model catalogs (no key — data only)

### OpenRouter public catalog — https://openrouter.ai/api/v1/models
- **Verified:** 2026-09-16T21:53:52Z — `GET` → **HTTP 200**, 734,899 bytes, **444 models, 20 `:free`-tagged** (e.g. `inclusionai/ling-3.0-flash-vl:free`).
- **Auth:** none for catalog; inference needs a free key (signup). **Region:** global (US).
- **CWI use case:** machine-readable map of which models have free tiers — guides key-signup prioritization.

### ModelDB (Axiom) — https://modeldb.axiom.co/api/v1/models
- **Verified:** 2026-09-16T21:55:27Z — `GET` → **HTTP 200**, 3.2 MB of model metadata with per-token costs, context windows, capabilities.
- **Auth:** none. **Region:** global (US).
- **CWI use case:** cost estimation + model selection for agent products; pricing intelligence.

---

## 10. Free speech AI — STT/TTS (no key)

### OVHcloud AI Endpoints — Whisper STT — https://oai.endpoints.kepler.ai.cloud.ovh.net/v1
- **Verified:** 2026-09-16T22:07:49Z — `POST /v1/audio/transcriptions` (multipart, model `whisper-large-v3-turbo`, no key), file = MP3 generated by Google TTS saying "The quick brown fox jumps" → **HTTP 200**, `transcription=" The quick brown fox jumps"` — exact match, full keyless TTS→STT round trip.
- **Auth:** none. **Region:** EU.
- **Free terms / limits:** anonymous tier, OpenAI-compatible audio endpoint.
- **CWI use case:** keyless speech-to-text for voice content pipelines, room/event transcription.

### Google Translate TTS — https://translate.google.com/translate_tts
- **Verified:** 2026-09-16T22:00:13Z — `GET /translate_tts?ie=UTF-8&client=tw-ob&tl=en&q=Keyless+test+one+two` → **HTTP 200**, `content-type: audio/mpeg`, 15,552 bytes of playable speech.
- **Auth:** none. **Region:** global.
- **Free terms / limits:** public web endpoint, no key. Unofficial API — be polite, don't hammer.
- **CWI use case:** keyless text-to-speech for content ops, accessibility, voice prototypes. (StreamElements TTS now requires a key — see DROPPED.md.)

---

## Taps this eliminates

For each currently-blocked CWI money step, the free alternative that removes or shrinks the block:

| Blocked step | Free alternative (verified above) | Residual block |
|---|---|---|
| Paid inference for lab multi-model runs | **Pollinations** (anonymous, live) + **AI Horde** (anonymous, live — 2nd keyless family) — run DNA harness across framings AND across model families today at $0 | A *third* keyless chat family is unverified: OVHcloud chat is documented-anonymous but 429-throttled from this IP; Hetzner free inference (EU, 500M tok/day) is one free signup away — see DROPPED.md |
| Paid hosting for receipt verifiers / storefronts | **GitHub Pages** (live) + **jsDelivr** (live) | None for static. Dynamic backends still need a host |
| Paid CI | **GitHub Actions** (live, running builds today) | None for public repos |
| Paid web search / scraping | **Jina Reader** + **DDG Instant Answers** (both live, keyless) | Heavy volume needs free keys (signup) |
| Paid chain RPC (Alchemy/Infura) | **sepolia.base.org** + **PublicNode** (both live, keyless) | Faucets for testnet funds still need signup (see DROPPED.md) |
| Paid geo/FX/price/translate data | **ipapi.co, Open ER API, CoinGecko, Coinbase, MyMemory** (all live, keyless) | Rate limits unmeasured — stay polite |
| Paid STT/TTS (ElevenLabs, Deepgram, etc.) | **OVHcloud Whisper** (live, keyless) + **Google Translate TTS** (live, keyless) — full voice round trip at $0 | Unofficial endpoints — stay polite; heavy volume needs a plan |
| x402 mainnet facilitator (CDP key = Black's tap) | **x402 testnet** (live, 10 routes, 402 flow proven) — the full loop builds and tests at $0 | Mainnet still needs Black's 4 taps; no free facilitator exists. Be honest about this. |
| Agent discovery rails | **Moltbook** (live, keyed) + **Agentic Market** (live) | Listing flows need signups |

**What $0 cannot do (stated plainly):** mainnet settlement, key-walled inference (Groq/Cerebras/OpenRouter-free-models/etc. — all 401 without signup), and any signup-gated free tier. Those are *one free signup* away, not one dollar away — the action list is signups, not spending.

---

*Registry built 2026-09-16 by the CWI Research Lab. Verification receipts are the product — challenge any entry by re-running its test.*
