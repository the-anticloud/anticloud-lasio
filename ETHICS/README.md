# Ethics — LASIO

**Project:** LASIO  
**Category:** OIL_GAS  
**Upstream:** https://github.com/kinverarity1/lasio  
**Pinned commit:** `20fb98d7e2c9444bbbc9ee0e7aff4420b7c5b512`  
**Assurance:** 16/16 checks passing  
**Ledger head:** `0beea607fd35d4094b0392a522cedc5f77547b1be90cb9eb77922ad1725a6f69`  
**Date:** October 2026

## Position

LASIO is packaged for offline deployment with a verifiable audit trail. The
ethical questions this raises are answered by making the system's behaviour
checkable rather than by policy statements.

## The four commitments

1. **No hidden egress.** The deployment has no external API dependency; this is
   testable by running it with the network disconnected.
2. **Attributable output.** Every artifact is recorded in a hash chain, so what
   the system produced can be reconstructed.
3. **Operator control.** The institution owns the hardware and the keys.
4. **Refusal to overclaim.** Where a certification is not held, the project says
   so rather than implying it.

## Dual use

This project is packaged for civilian and public-sector deployment. Where an
upstream has dual-use characteristics, the licence gate and the reference-only
marking in `BENCH.json` record that.
