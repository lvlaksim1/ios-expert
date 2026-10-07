# Next

1. Redesign the PP-RM/GitHub gate so one Scheduled-Task wake performs one durable transition only: reserve -> separate effect wake -> separate evidence wake -> separate acceptance wake -> separate recovery/verification wakes.
2. Re-run the gate with the same fail-closed criteria: single reservation winner, exactly one logical effect, separate evidence/acceptance, injected unknown outcome, recovery without repeating effect, no double credit, >=5 seconds between sequential requests.
3. Establish a technically separate evaluator identity/access boundary for hidden assessments. Same GitHub identity, another branch/path/repository or readable Git history do not count.
4. Run a non-sensitive canary denial test: evaluator can read canary; training identity cannot read it through any permitted path.
5. Only after both infrastructure gates pass, create the first hidden baseline assessment instance.
6. Run baseline diagnosis against Owner-approved profession-map v0.3.0 / target-profile v0.2.
7. Build the first learning program from the observed gap map.
