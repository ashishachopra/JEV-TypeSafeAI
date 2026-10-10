# https://docs.typesafe.ai/introduction

# Awesome Jev Use Cases
LLMs write essays. Jev makes the call. This is the community's living index of what people are actually shipping with TypeSafe AI's System One decision model: real repos, real measurements, and the patterns that already work.
Jev is TypeSafe AI's first System One model: a decision engine that returns typed, calibrated judgments (Choice / Score / Noul) instead of free-form prose. It runs in 70–500 ms at ~$0.042 per million input tokens, and output tokens are free. Fast enough to sit inside a game loop, cheap enough to run over millions of rows, and constrained enough that your code can branch on the answer without parsing JSON.
Every listing links to a public source. Headline results are tagged [self-reported] or [independent], and every link is scored against a written rubric before it lands here (see CONTRIBUTING.md).

JevTypeSafe AISystem One Decision ModelUse CasesAI Agents

# What is Jev
You send Jev a state (a string, JSON object, or list of text) plus typed questions. It returns typed answers with probabilities: no invented fields, no malformed JSON, no off-schema values. Your code owns the control flow, the thresholds, and the side effects.

|Primitive|You declare|Jev returns|
|Choice|A list of options (up to 255)|The chosen option + probability per option + confidence
|Score|An ordered rubric (2–10 levels)|A probability-weighted score + confidence
|Noul|A yes/no statement|A single probability from 0 to 1

Three primitives is the whole API. That's the point. Questions in one request are evaluated in parallel and in isolation against the same state, so asking ten questions costs roughly the time of one. That one property unlocks speculative fan-out, confidence-gated routing, and every pattern on this list.
The economics (vendor-reported): $0.042 / million input tokens, output free, 70–500 ms end-to-end. On TypeSafe's own four-workflow eval, Jev lands at 67.8% agreement with a frontier-model consensus at $0.0004 per case: essentially tied with GPT-5.6 Terra (67.9%) at ~1/76th the cost. Treat the multipliers as directional, not gospel: the honest independent numbers are lower.

# Official Resources
## DOCUMENTATION
https://typesafe.ai/ </br> https://typesafe.ai/blog/introducing-system-one-models-and-jev </br> https://docs.typesafe.ai/introduction </br> https://docs.typesafe.ai/api
</br> https://docs.typesafe.ai/primitives </br> https://docs.typesafe.ai/patterns </br> https://docs.typesafe.ai/models </br> https://docs.typesafe.ai/demos </br> https://console.typesafe.ai/playground
https://evals.typesafe.ai/ </br> https://console.typesafe.ai/login
## SDK
https://github.com/typesafe-ai/typesafe-sdk-python </br> https://github.com/typesafe-ai/typesafe-sdk-js </br> https://github.com/typesafe-ai/system-one-adapter-python </br> https://github.com/typesafe-ai/skills|

# Top Use Cases
The use cases with the most traction since launch: ranked by popularity, not raw star counts (stars are a hidden ordering signal only; rigor does not track reach).

🔥 Top 
</br> * browser-use/jev-ultrafast (browser agent · Zürich → London Google Flights in 7.1 s / $0.0039)
</br></br> * tamaratran/fast-jev-compaction (Claude Code compaction → Jev keep/delete · content stays verbatim)
</br></br> * jarrodwatts/jev-trader (market maker on Monad/Kuru · 81 ms latency per block)
</br></br> * awlevin/typesafe-computer-use (macOS computer use · $0.0002 / decision vs Opus 5 at $0.032)
</br></br> * thruwire/foreman (supervisor over Codex workers)
</br></br> * devagrawal09/jev-review (staged code reviewer + dashboard)
</br></br> * fhshaik/typesafe-mario (Super Mario from emulator RAM)

⚡ Rising
</br>The "few upcoming": high rubric score but below the popularity cutoff. This tier is where rigor beats reach: several of these have single-digit stars and the strongest measured results.
</br></br> * realZachi/pg-jev (natural-language PostgreSQL WHERE · 129 rows in ~1 s for ~$0.0009)
</br></br> * droidrun/mobile-jev (Android agent · Uber route in ~21 s / 9 actions)
</br></br> * DevMortimer/pi-warden (steering guardrails · 6 rule breaks → 0 across 150 paired runs)
</br></br> * AnshChoudhary/typesafe-ai-firewall (tool-call firewall · 0% hard negatives blocked vs 39.2%)
</br></br> * moritzkremb/jev-voice-browser (voice control of a real browser · acts before the sentence ends — 34/34 live intents)
</br></br> * AbdelStark/heist-one (stealth game, per-guard Jev judgments · 12/12 live runs, 288 typed judgments, 0 fallbacks)
</br>Every headline result is self-reported by the project author: launch-week proof-of-concept signal, not production case studies.

# Community Builders
The long tail of unique use cases, grouped by decision shape. Each entry answers two questions: what does it do, and why is it unique.

# 01 Workflow
</br>Smart if-statements inside ordinary software: the fuzzy middle between brittle rules and expensive chat models.

</br> * kylemclaren/jevql: SQL WHERE jev(...) filters on vanilla Postgres. Unique: SQL filtering without a plugin or embeddings. [self-reported]
</br></br> * AboveColin/HA-Jev: Home Assistant integration. Unique: a decision layer for household automations. [self-reported]
</br></br> * valentynkit/jev-commit: commit message accuracy checks. Unique: pre-commit semantic lint instead of a full review. [self-reported]
</br></br> * valentynkit/jev.nvim: plain-language buffer search in Neovim. Unique: semantic editor search with no embeddings. [self-reported]
</br></br> * kylemclaren/jevsearch: shadcn/ui ⌘K site-search block; a local keyword pass streams hits, then one Jev request re-ranks the top 20 with a Noul per page, a Choice for the best answer, and a Noul for whether any page answers the query. Unique: site-search re-ranking with no embeddings or vector DB (Hit@1 83% vs 41% for Lunr on 41 labelled queries over the TypeSafe docs). [self-reported]
</br></br> * DanRWilloughby/snifftest: prose linter for AI-writing tells. Unique: one probability per rule, and it never rewrites your text. [self-reported]
</br></br> * zephel01/Jev-sample: question-shape demo (a 4-option Choice scores 48.3%; decomposing into four precondition Nouls reaches 98.3%). Unique: quantifies the atomic-question decomposition payoff. [self-reported]
</br></br> * mrnugget/jev-shell-history: Fish-style Zsh history autosuggestions ranked by Jev from the current input. Unique: semantic shell-history ranking with no embeddings. [self-reported]
</br></br> * wustep/jev-playground: Jev chooses bounded musical attributes (enums only) while code renders sheet, audio, and MIDI. Unique: enum-bounded music steering — the decision layer, not the notes, is the model's job. [self-reported]
</br></br> * kylemclaren/jevpdf: ask a PDF in your own words in the browser; pdf.js extracts lines locally, each line gets one Jev Noul (batched up to 16 lines per request with the page as context), and matching lines highlight page by page ranked by probability. Unique: plain-language Ctrl+F for PDFs; Jev only sees extracted text, never the file. [self-reported]
</br></br> * asfarsadewa/human-compiler: a browser "compiler" for human language — a local lexer splits pasted text, then one Jev request (many Nouls, Choices and Scores) emits rustc-style diagnostics with codes, spans and severity, and code decides what fires. Unique: the model supplies measurements only, so identical measurements produce identical diagnostics; mode profiles (corporate/manager/linkedin/academic/reddit/politician/teenager) are lint profiles with their own thresholds. [self-reported]
</br></br> * Canonical examples (TypeSafe cookbook): insurance FNOL / claims triage, KYC & financial-crime checks, e-commerce listing normalization, returns approval, sales lead/ICP scoring, support-ticket triage — official use-case map.

# 02 Bulk
</br> * Cheap judgment over giant corpora: the economics that make "run it on everything" rational.
</br></br> * valentynkit/jev-skip: YouTube sponsor-segment detection from captions. Unique: crowd-free sponsor detection (77% of SponsorBlock's seconds). [self-reported]
</br></br> * youkiti/tiab-review-plugin: title/abstract screening for systematic reviews. Unique: evidence-synthesis triage at scale (95% recall @ 16,645 records). [self-reported]
</br></br> * kitze/Unclutter: per-element DOM classifier (keep/ad/cookie/promotion/newsletter/social/uncertain). Unique: browser decluttering as a shipped job; no other entry covers UI hygiene. [self-reported]
</br></br> * dani1005/book-aurora: scores a novel's passages across nine emotions plus overall intensity, visualized as an emotional aurora. Unique: whole-book emotion scoring — every passage becomes a row of colour. [self-reported]
</br></br> * Tatuck/jev-boe-demo: screens Spain's official gazette (BOE) daily, scoring public impact, classifying topics, selecting summary paragraphs. Unique: daily legal-gazette screening with impact scoring. [self-reported]
</br></br> * reachjalil/jevlogs: OpenTelemetry log triage — wraps an existing OTLP exporter, scores each log's diagnostic value (0–100), priority and actionable probability with Jev, and annotates records with jev.* attributes so low-value logs can skip a separate LLM-analysis branch. Unique: observability log triage at the collector; only body/severity/service reach the model after redaction. [self-reported]
</br></br> * ChetasLua/jevmeter: scores every sentence of a video with one Jev request per sentence across preset question sets (BS/SPIN/HOT-TAKE/HYPE), then renders a 16:9 edited video with meter, flags and scoreboard via ffmpeg. Unique: end-to-end media pipeline (Whisper transcription + per-sentence Nouls + highlight selection + resumable cache). [self-reported]
</br> * Canonical examples: 1,018 papers → 24 topics for ~$0.08; 2,000 wine notes → CatBoost numeric features at 1.77 RMSE.

# 03 Realtime
</br>Action selection at game, UI, and market clock rates: perception and safety stay in code, Jev picks the move.
</br></br> * phyous/tsai-sc: StarCraft shareware harness. Unique: real-time strategy from structured game state. [self-reported]
</br></br> * valentynkit/jev-plays-pokemon-red: Pokémon Red decisions scored by Brier against RAM. Unique: calibrated in-game decision logging. [self-reported]
</br></br> * RomanSlack/jev-drone: camera-only quadrotor. Unique: split-rate control (tactical vs safety loop). [self-reported]
</br></br> * sorrycc/typesafe-snake: Snake where Jev picks each move from structured game state. Unique: the first linked implementation of a canonical realtime example. [self-reported]
</br></br> * Reisenbug/TerraBlind: a pre-launch Terraria tModLoader mod that added Jev to fight the bosses — one question every 200 ms, code turns the answer into keystrokes. Unique: an established game mod adopting Jev as its boss-fight decision layer, plus a code-only fresh-world pipeline. [self-reported]
</br></br> * cwdx/1-million-emojis: shared 1,000 × 1,000 emoji canvas (live); after each human stroke, one Jev request answers a Choice over named (emoji, place) options beside it and a Noul on whether the stroke is an unfinished shape, and code finishes the shape above 0.7 or samples the pick from the probabilities. Unique: Jev as a co-painter answering many humans in one realtime multiplayer canvas, not an agent playing alone. [self-reported]
</br></br> * asfarsadewa/werewolf: Werewolf against seven villagers whose suspicions are calibrated Jev probabilities; each message is measured by one Jev request and every villager keeps a visible, updateable suspicion probability. Unique: social-deduction belief state as typed probabilities; deterministic (seed + measured actions), ~750 authored lines, no generation. [self-reported]
</br></br> * lbotinelly/jev-little-airways: a toy archipelago ATC sim where every in-flight call (continue/divert/hold, declare an emergency, give way, clearance, landing order) is a batched live Jev request every ~1.6 s (~150 ms answers), with runway exclusivity kept in deterministic code. Unique: multi-agent realtime ATC with a live Jev monitor (raw request/response, latency, tokens, cost) and documented question-wording/confidence findings. [self-reported]
</br>Canonical examples: Doom (~10 Hz), Wikiracing, Snake, Tetris, Pac-Man, Subway Surfers ×50.

# 04 Verify
</br>Score, judge, and gate prompts, traces, tool calls, and claims: at a fraction of the LLM call you're protecting.
</br></br> * valentynkit/jev-belay: blocks an unverified "done" in a coding agent. Unique: evidence-gated task-completion guardrail. [self-reported]
</br></br> * kiarina/labs: safety judgment: moderation plus shell-command checks. Unique: strong Japanese moderation (36 vs 292 misses). [self-reported]
</br></br> * teyhouse/jev-secret-detection: secret/credential scanning in code and text. Unique: a dedicated secret-detection decision, distinct from shell-command safety and agent guardrails. [self-reported]
</br></br> * Red5d/jev-cvss: extracts CVSS v3.0/v3.1/v4.0 metrics from vulnerability descriptions and scores deterministically. Unique: structured CVSS extraction — Jev parses, code computes. [self-reported]
</br></br> * supercorp-ai/supercov: coverage, security and code quality for coding agents; Jev checks each source file so the agent knows what to fix first. Unique: twelve named quality and twelve named security questions of every source file, each security check mapped to CWE classes, with files ranked for the agent next to their test coverage. [self-reported]
</br></br> * qkal/canny: ledger-first agent supervision hooks for Claude Code and Codex; deterministic blockers (missing passing check, secret patterns) gate the loop while optional Jev Noul judgments advise, with canny replay re-reading the append-only ledger. Unique: Jev judgments never sole-block — deterministic checks decide and Jev only advises. [self-reported]
</br></br> * devanshbatham/commit-miner: classifies Git commit diffs and messages with Jev — bug fixes, security fixes mapped to CWEs, and change types; scans a local repo or GitHub clone and emits HTML/CSV reports with estimated Jev cost. Unique: post-hoc corpus-wide commit classification + CWE mining, distinct from the pre-commit single-Noul valentynkit/jev-commit. [self-reported]
</br>Canonical examples: citation grounding, jailbreak and prompt-injection screening, pre-execution shell checks.

# 05 Harness
</br>Make the agent loop cheaper, safer, and composable: Jev as the load balancer above models, tools, and humans.
</br></br> * jkudish/jev-mcp: MCP server for coding agents. Unique: verification + injection screening over MCP. [self-reported]
</br></br> * itsmostafa/typesafe-mcp: single-binary Go MCP. Unique: zero-dependency agent integration. [self-reported]
</br></br> * AbdelStark/bicameral: Pi harness with typed reflexes. Unique: a decision layer as the coding-harness reflex arc. [self-reported]
</br></br> * jexp/neo4jev: navigates a Neo4j graph one relationship at a time via a classifier over neighbouring relationships. Unique: graph traversal as a typed decision, hop by hop. [self-reported]
</br></br> * xinyao27/jevonian: Local OpenAI/Anthropic/Responses-compatible proxy where one Jev call answers both the model route and the thinking level for its jevonian/auto model, after code has filtered candidates by protocol, context window, effort floor, and spent quota windows; a pinned model or explicit route skips Jev entirely, and each turn is logged with the serving model, reason, token usage, and estimated cost. Unique: the decision is a cost-and-cache one, not just a capability one, and it stays auditable. [self-reported]
</br></br> * suenot/codex-jev-router: Uses Jev Choice and Noul decisions on short task summaries to select the model and reasoning effort when Codex spawns a subagent. Unique: installs an instruction-driven Codex subagent workflow with local confidence gates and backup/rollback. [self-reported]
</br></br> * hyperspaceai/jevcache: local memoization plus an audit/replay ledger for Jev decisions keyed by (model, schema, state hash), with a decide/recall/replay/serve CLI and a local key rather than a proxy. Unique: a local memoization-and-replay harness for decision calls, not another routing proxy. [self-reported]
</br></br> * reachjalil/jev-tree: recursive Jev Choice over a taxonomy — walks a JSON tree so thousands of leaves are selectable even though one Choice caps at 255 options, and auto-buckets oversized siblings. Unique: directly solves the 255-option cap by recursion (default fanout 32); timeouts fail to reason: unavailable instead of inventing a leaf. [self-reported]
</br>Canonical examples: skill routing, context reduction, model routing.

# 06 Voice
</br>Sub-second decisions on the audio path: the youngest pillar, still mostly conceptual.
</br></br> * santos-sanz/jev-audio-beeper: low-latency audio-censorship POC — a Jev Boolean (isInsult) plus a Score (severity) per token identifies Spanish profanity, and matching word intervals are beeped with ffmpeg without changing duration. Unique: a streaming audio-path decision (bounded look-ahead buffer, hysteresis, fail-open/closed as a product choice) with a JSON audit report — the first repo in the Voice pillar. [self-reported]
</br></br> * Spoken "go back" mapped to a click in ~300 ms (voice → action)
</br></br> * End-of-utterance and turn-taking detection via a Noul
</br></br> * Speak-up gates for wake-word-free assistants
</br>The first Voice repo has landed; this is still a young pillar to watch.

# Benchmarks
</br>Rigor over reach. Everything here is tagged independent or self-reported.
</br>
## Independent evaluations
</br> * largitdata: "Jev System One Model open-source benchmark": multi-turn RAG routing — Gemma 4 31B vs Jev vs open alternatives; latency advantage for Jev. [independent]
</br></br> * priorbench/jev: "Independent pre-registered evaluation of Jev": pre-registered run via OpenRouter — 50 predictions, 5,721 calls, 21 experiments; 95.9% zero-shot, ~430 ms floor, 0.97 confidence on random letters; raw outputs + recount script. [independent]
</br></br> * decisioneval.dev: "Frozen-split evaluation of Jev 1.13.0": 400 cases / 2,000 decisions — acc 0.740, Brier 0.148, ECE 0.045, abstention curves, CIs; teacher-ensemble labels. [independent]
</br></br> * arXiv:2609.37647: “Evaluating and Benchmarking the System One Model Jev”: 37 datasets, 346,009 requests under $10; code + raw responses. [independent]
</br></br> * arXiv:2609.33209: “Beyond Calibration: Do a Typed-Decision Model’s Probabilities Obey the Probability Axioms?”: probability-axiom/coherence audit — negation/exclusivity violations, exactly at bar. [independent]
</br></br> * arXiv:2610.01006: “Beyond Answer Confidence: A Controlled Audit of Self-Knowledge in a Black-Box Decision Model”: confidence up to 0.80 with no answer-relevant information; on post-knowledge-boundary news confidence exceeds accuracy by 0.21–0.33; an explicit “evidence suffices” question reaches AUROC 0.95 vs 0.85. [independent]
</br></br> * arXiv:2609.40241: “Decision-Oriented Recommendation Reranking: An Empirical Study of Jev”: strong recommendation effectiveness on Amazon Reviews; more gradual latency growth than pointwise Qwen, but substantially slower than specialised recommenders. [independent]
</br> * daf-jev: Python toolkit + live-API characterization — batching ~18× speedup / ~4× fewer tokens, calibration, MCP server. [independent]

## Benchmark repos
</br> * jev-sec-bench: 96.5% injection accuracy, ECE 0.0588 [self-reported]
</br></br> * jev-agent-failure-benchmark: beat GPT-5.4 on every axis, $1.28 [self-reported]
</br></br> * jev-rerank-bench: nDCG@10 0.692 vs Cohere 0.691 (tie) [self-reported]
</br></br> * jev-phishing-bench: 2,000 emails vs Claude Haiku 4.5 [self-reported]
</br></br> * typesafe-ai-benchmark: Jev vs Qwen 3.8 27B [self-reported]
</br></br> * jev-eval-agent: public eval harness [self-reported]
</br></br> * jev-dspy-lab: DSPy companion [self-reported]
</br></br> * andreylukin/jev-bcp: BrowseComp-Plus agent pipeline using a cheap LLM plus Jev for grading (AUC 0.94, ECE 0.045), answer checking (AUC 0.90), passage picking and trajectory selection; the jevlog experiment DSL and every experiment are included, null results and all (its jevlog DSL is unrelated to reachjalil/jevlogs in 02 Bulk). [self-reported]

## Open re-implementations
</br> Reproducing the interface, not the weights: proof that the decision-layer idea travels.
</br></br> * TheoLeeCJ/SemIf (was "openjev"): frozen 4B model, reads option logits
</br></br> * vinnylarouge/jevlike: one-pass scorer
</br></br> * Mapika/decider: Qwen3.5-2B fine-tune
</br></br> * NullPo-jp/PocketJev: on-device iPhone (MLX + Qwen3-VL)
</br></br> * Laya: Apache-2.0 open alternative, 3 checkpoints, runs on a free Colab T4 (421M params, ModernBERT + decision head; author-reported ~35 ms, earlier listed as ~30 ms; vs ~302 ms, 0.590 vs 0.974 accuracy). GitHub · demo
</br></br> * com-kotobalabs/open-jev-deberta-v3-large: open reproduction on DeBERTa-v3-large (self-hostable)
</br>Watch: the Jev Decision Index on Hugging Face follows every open-weight reproduction attempt.

# Popular Blogs
</br>The writing worth reading, ranked by writer popularity × content uniqueness. SEO recaps are excluded by design.
</br> * https://every.to/vibe-check/mini-vibe-check-typesafe-s-jev-judged-everything-i-ve-written-in-0-7-seconds
</br> * https://techcrunch.com/2026/09/18/a-new-kind-of-ai-model-from-a-chatgpt-inventor-is-thrilling-developers/
</br> * https://flaviocopes.com/jev/
</br> * https://archerhume.com/posts/jevs-architecture-unmasked/
</br> * https://www.latent.space/p/ainews-jev-a-system-one-model-that
</br> * https://www.theregister.com/ai-and-ml/2026/09/16/typesafe-ai-debuts-model-for-machines-that-plays-doom/5296711
</br> * https://ts2.tech/en/typesafe-ai-raises-40-million-for-jev-but-its-445x-cost-claim-is-still-self-tested/
</br> * https://kingy.ai/blog/typesafe-jev-review-the-ai-model-that-doesnt-generate-text/
</br> * https://dev.to/valyuai/how-to-use-jev-a-practical-guide-to-typesafes-system-one-model-g5e
</br> * https://www.orcarouter.ai/blog/jev-typesafe-system-one-what-we-know
</br> * https://www.datacamp.com/blog/system-one-models-jev
</br> * https://agentjournal.dev/blog/llm-judge-vs-feature-extraction/
</br> * https://www.langchain.com/blog/building-a-harness-with-jev
</br> * https://x.com/CompleteSkeptic/status/2099925682726002904
</br> * https://news.ycombinator.com/item?id=49717558
