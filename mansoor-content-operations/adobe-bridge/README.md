# adobe-bridge (Eddie VM)

Pairs with Mini `/Users/ivanclawd/mve-adobe`.

- `packages/` immutable job packages before submit
- `queue-out/` staging before scp to Mini `queue/incoming`
- `results-in/` pulled Mini `results/`
- `fixtures/` synthetic sources/XML for Stage 2–4
- `evidence/` smoke proofs (also copied under EDDIE BRAIN/MVE_PROJECT_SYSTEM/adobe_bridge_evidence)
- `xml/` generated Premiere XML
- `scripts/` VM submit/readback CLIs

Mini tree: queue/{incoming,claimed,done,failed}, staging/{sources,proxies,tmp}, projects, exports, fixtures, evidence, worker/{bin,logs,locks}, tools (app + ffmpeg symlinks).
