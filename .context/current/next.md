# Next

1. Run PP-RM/GitHub gate run 2 using one durable transition per tick.
2. Preserve run 1 unchanged as negative evidence.
3. Required transition chain for run 2: reserve -> effect -> evidence -> acceptance -> injected-unconfirmed effect -> reconcile -> final verify.
4. Every transition must fail closed if the canonical predecessor state is not exactly what it expects; no task repairs a previous task.
5. Enforce >=5 seconds between sequential external requests inside a tick.
6. After PP-RM gate passes, run the assessment runtime-separation canary with multi-tick preparation and multi-tick solving and verify `P ∩ S = ∅`.
7. Only after both gates pass, run baseline diagnosis against Owner-approved profession-map v0.3.0 / target-profile v0.2.
8. Build the first learning program from the observed gap map.
