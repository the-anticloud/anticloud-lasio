# Students — LASIO

**Project:** LASIO  
**Category:** OIL_GAS  
**Upstream:** https://github.com/kinverarity1/lasio  
**Pinned commit:** `20fb98d7e2c9444bbbc9ee0e7aff4420b7c5b512`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `0beea607fd35d4094b0392a522cedc5f77547b1be90cb9eb77922ad1725a6f69`  
**Date:** October 2026

## What this project gives you

A complete worked example of offline-first packaging with a cryptographic audit
chain: source pinned at `20fb98d7e2c9444bbbc9ee0e7aff4420b7c5b512`, a 16-check assurance suite, an evidence register
with per-check hashes, and an AIOSS ledger chain ending at `0beea607fd35d4094b0392a522cedc5f77547b1be90cb9eb77922ad1725a6f69`.

## Learn by verifying

```
python tools/run_bench.py --out BENCH.json
```

Then take any row from `ISOLATED_LAB_RESULTS/03_Result_Register.md`, recompute
the SHA3-256 of its evidence file, and confirm it matches. If it does not match,
the record has been altered — that is the whole point of the chain.

## Licence

Apache 2.0 terms apply to study and teaching use.
