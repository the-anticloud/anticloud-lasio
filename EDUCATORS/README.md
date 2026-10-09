# Educators — LASIO

**Project:** LASIO  
**Category:** OIL_GAS  
**Upstream:** https://github.com/kinverarity1/lasio  
**Pinned commit:** `20fb98d7e2c9444bbbc9ee0e7aff4420b7c5b512`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `0beea607fd35d4094b0392a522cedc5f77547b1be90cb9eb77922ad1725a6f69`  
**Date:** October 2026

## Teaching with LASIO

The project is usable as a worked example of offline-first packaging with a
cryptographic audit chain. It ships with the assurance suite, the evidence
register and the ledger, so students can verify claims rather than take them on
faith.

## Suggested exercises

1. Run `python tools/run_bench.py --out BENCH.json` and read the 16 results.
2. Recompute the SHA3-256 of a row's evidence file and compare to the register.
3. Walk the AIOSS chain from genesis to head `0beea607fd35d4094b0392a522cedc5f77547b1be90cb9eb77922ad1725a6f69` and confirm every link.
4. Break one artifact and observe the chain fail to verify.

## Licence for teaching

Apache 2.0 terms apply to academic and teaching use. See `24_ANTICOMMONS_LICENSE`.
