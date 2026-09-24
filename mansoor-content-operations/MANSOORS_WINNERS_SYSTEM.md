# Mansoor's Winners — always-on TOF system

Updated: 2026-09-09

## Outcome

The Mac mini continuously discovers, analyzes, proposes, assembles, and learns from TOF concepts. It may research and render unattended, but it never promotes an idea into production, publishes a post, or exposes Mansoor's wife's face without the existing approval and privacy gates.

The system is a loop, not a one-time content scrape:

`discover -> capture evidence -> analyze -> cluster -> approve concept -> map assets -> assemble -> QC -> Slack review -> approve -> Drive ready-to-post -> measure -> learn`

## Current baseline

The Notion database [Mansoor's Winners](https://app.notion.com/p/1e1768da476049818427b246504e1e60) is the research memory for Mansoor's own proven posts. It is intentionally separate from the production queue.

Public Reels grid snapshot from `@mansooralzayer`, observed 2026-09-09:

| View tier | Reels |
| --- | ---: |
| 5–10K | 66 |
| 10–50K | 28 |
| 50–100K | 0 |
| 100K+ | 6 |
| **Total >=5K** | **100** |

All 100 records have the observed view count, tier, shortcode, and source URL. The six 100K+ posts have a browser-evidence analysis pass. Lower tiers remain `Indexed` until their visual/audio evidence is acquired and analyzed.

## Proven patterns from the 100K+ tier

### 1. Family payoff beats luxury flex

The largest result (854K) and an earlier 185K version use the same little-sister reveal. The visual proof is expensive, but the emotional subject is the sister. The viewer reads the moment as what persistence did for a loved one, not merely what Mansoor owns.

Reusable formula:

`specific sacrifice -> visible proof -> loved one's reaction`

### 2. A whole creative shell can be repeated

Three winners use the same audio ID (`1275631570518872`), the exact overlay `Behind every successful man..`, and the same sparkling Rolls-Royce night composition:

- grandfather story: 222K
- father story: 185K
- grandfather repost: 123K

The relationship/caption changed once, and a near-exact repost also won. Therefore the system needs template-family IDs, audio IDs, asset IDs, deployment history, and cooldown rules. It must not assume originality is always superior to controlled reuse.

### 3. POV language makes success viewer-shaped

`POV: The moment you show her...` turns a private achievement into a scene the viewer can imagine creating for their own family. The line is short enough to understand without sound and specific enough to create an emotional promise.

### 4. Vulnerability creates conversation

The 190K origin montage begins with `How demanding are your dreams?` and shows archival footage from a business failure. It had a much stronger comment count than the short reveal posts. This is a separate template family: documentary transformation, not lifestyle B-roll.

### 5. Captions deepen; they do not rescue

The winning first frame already works. Captions add the homelessness, Prius, grandfather investment, or tough-love context. A long caption cannot compensate for a weak first three seconds.

## What the existing copycat documentation gets right

The local TOF copycat skill correctly requires Share, Picture, Library, Audio, and ICP gates. The winners add three operating requirements:

1. Track recurring **template families**, not isolated URLs.
2. Store the Instagram **audio ID**, because display names are unstable and the same audio can recur.
3. Maintain a **winner-recycling lane** for Mansoor's own proven masters.

Translation remains mandatory. Copy the causal mechanism, pacing, text density, and emotional job. Do not copy another creator's exact wording, identity, claims, or world.

## Source lanes

### A. Owned winner monitor

- Scan Mansoor's published reels.
- Snapshot views and visible engagement at 24h, 72h, 7d, and 30d when accessible.
- Upsert by shortcode; never create duplicates.
- Promote >=5K into the four requested tiers.
- Re-analyze when a post crosses a tier or materially changes the account baseline.

### B. Trial reel monitor

- Trial reels are a separate private inventory.
- Desktop Chrome exposes owner insights per published reel but did not expose a trial-reels list during the 2026-09-09 audit.
- Use an authenticated mobile acquisition worker on the spare phone if the phone is provisioned. Capture only metadata and evidence needed for the workflow; do not weaken the phone's security or store reusable credentials in the repository.

### C. External copycat scout

- Preferred: Sandcastles piles/channel/search workflow described by the local copycat skill.
- Eligibility default: >=100K and >=2x creator baseline; fallback >=25K and >=1.5x only when the strict pass is empty.
- If Sandcastles is unavailable, accept explicit Instagram URLs from a Slack research inbox. Label them as manually sourced; do not pretend a generic web search is Sandcastles evidence.

### D. Slack idea inbox

- Accept a reel URL, file, screenshot, or written idea.
- Acknowledge with a receipt containing the canonical source URL, source lane, created record, and next state.
- Research intake creates a winner/candidate record. It does not auto-create a production task.

## Worker design

### 1. Supervisor

One launchd-managed service on the Mac mini owns a durable SQLite queue. Workers claim idempotent jobs with leases and exponential retry. A watchdog restarts unhealthy workers. Secrets live in Keychain or environment files outside the repository.

Suggested job types:

- `discover_owned_reels`
- `discover_trial_reels`
- `ingest_slack_candidate`
- `acquire_instagram_evidence`
- `analyze_winner`
- `cluster_patterns`
- `draft_copycat`
- `map_broll`
- `assemble_tof`
- `qc_render`
- `deliver_slack_review`
- `promote_approved_to_drive`
- `snapshot_performance`

### 2. Evidence acquisition

Every analysis packet should contain:

- canonical URL and shortcode
- observed timestamp and view count
- creator baseline/outlier multiple
- exact overlay/OCR with confidence
- caption and visible engagement
- audio display name and stable audio ID
- first, middle, and final frame contact sheet
- duration, shot boundaries, aspect ratio, and text-safe zones
- privacy/claim/audio-rights flags

If a field is unavailable, store `unknown` with the acquisition reason. Never fill it by inference.

### 3. Winner analyzer

The existing Idea Analyzer is a routing analyzer for Asana ideas. It is not sufficient for winner forensics. The winner analyzer should emit a strict packet containing:

- format and template family
- exact hook/wording and text geometry
- beat-by-beat structure
- audio ID, musical role, energy curve, and clean/profane status
- imagery, shot function, camera movement, and transition behavior
- emotion, identity, status, curiosity, proof, and sharing mechanism
- caption mechanism and CTA
- reusable causal pattern vs creator-specific decoration
- ICP translation
- B-roll library slots and missing-asset list
- copycat score and rejection reasons
- confidence and evidence references for every non-obvious claim

### 4. Pattern miner

Cluster by normalized hook, audio ID, template family, first-frame composition, beneficiary, emotional promise, duration, and B-roll asset family. Report:

- recurring audio and its median/maximum performance
- repeated wording and successful variants
- exact/near reposts
- visual motifs associated with tier jumps
- template fatigue and recommended cooldown

## Production path

### Concept gate

A candidate enters `Copycat Pipeline — Ideas for Review` only after it passes the local Share/Picture/Library/Audio/ICP gates. Human approval is required before `Ready to Edit`.

### Assembly engine

For 6–15 second TOF B-roll, use deterministic assembly first:

1. choose a proven template family;
2. fill named B-roll slots from the library;
3. place exact approved on-screen text inside title-safe bounds;
4. cut on the template beat map;
5. mix or replace approved audio;
6. render a vertical review master and evidence/contact sheet.

Use FCPXML/Premiere XML when a human editor may refine the timeline. Use direct FFmpeg stitching for simple locked templates. Both paths must produce the same manifest: source asset IDs, in/out points, text, audio, fonts, crop decisions, and render hash.

### QC and delivery

Before Slack delivery, verify:

- 1080x1920, expected duration, valid audio, no black/frozen frames
- overlay spelling and safe margins
- first-three-second picture match
- no unsupported claims or dirty/trending audio surprises
- no visible wife face and no accidental private information
- B-roll diversity and no unapproved duplicate deployment

Send review renders to the existing video-review Slack route with the concept receipt and manifest. Only an explicit approval event moves the approved export into the dated Google Drive ready-to-post folder. Publishing remains a separate authorized action.

## Throughput policy

“Always on” should mean continuous discovery, analysis, asset indexing, and rendering—not unlimited posting. Keep a rolling buffer of approved concepts and renders, while daily output is capped by the content calendar and review capacity. Backpressure pauses drafting when the review queue is full.

## Learning loop

After publication, join the post back to its source winner, template family, audio ID, hook variant, and exact render manifest. Compare 24h/72h/7d/30d results to Mansoor's rolling median. Promote templates based on repeated evidence; retire them for fatigue or brand risk. Every approved or rejected draft becomes training evidence for the next scoring pass.

## Current blockers before unattended production

1. Sandcastles is documented but no Sandcastles MCP/tool is connected on this Mac.
2. Instagram media download through the existing CLI failed because Chrome's encrypted cookies were not available to `yt-dlp`; browser inspection works, but the evidence-acquisition worker needs an authenticated supported path.
3. The local Idea Analyzer and constants contain `/home/box/...` paths from the Linux deployment, so the exact wrapper is not portable to this Mac copy.
4. Trial reels appear to require an authenticated mobile surface.
5. The approval event, Slack review listener, and post-approval Drive mover need one canonical receipt contract so no worker infers approval from conversation text.

## Recommended implementation order

1. Make acquisition reliable: Instagram owner web insights plus mobile trial-reel worker; connect Sandcastles.
2. Make the existing analyzer paths configurable and add the winner-forensics schema.
3. Build the durable queue, dedupe, receipts, and Notion upserts.
4. Index the B-roll library into searchable shot-level assets.
5. Implement one deterministic `Family payoff POV` template end to end.
6. Wire Slack approval to Drive promotion.
7. Add performance snapshots and pattern-learning reports.
8. Expand to `Behind every successful man` and documentary origin templates only after the first lane passes real reviews.
