# Corrections

## 25 Nov 2026: 12-qubit GHZ fidelity bound (lesson 05, notebook)
The 12-qubit GHZ experiment (job `dc31a72nj2vs73dhgo10`, dataset folder `data/18-twelve-qubit-ghz-christmas-lights`) was
pre-registered with the fidelity estimate (P_sync + <X...X>)/2. That formula is **not a valid lower bound** on GHZ fidelity:
a product state such as |+>^12 has P_sync = 1/2048 and <X...X> = 1, so it would score about 0.5 while its true GHZ fidelity
is 2^-11. The valid two-setting bound is F >= P_sync + (<X...X> - 1)/2 (Toth and Guhne, PRL 94, 060501 (2005)).

Recomputed from the same saved counts (no new hardware run): P_sync = 0.77325, <X...X> = 0.519, so F >= 0.53275, with
shot-noise standard error 0.0095 (about 3.5 standard deviations above 0.5, assuming trusted, consistent measurements).
The pre-registered prediction, recomputed from its saved components, is 0.55495. The original pre-registration and results
files are unchanged; this is a post-run correction of the derived quantity. Lesson 05 and the notebook now use the valid
bound. Pooled accuracy across 49 comparisons changes from a mean absolute miss of 2.57 to 2.55 points.

Thanks to the reviewer (Codex) who caught it.
