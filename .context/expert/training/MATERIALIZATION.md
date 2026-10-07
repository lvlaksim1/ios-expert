# Training baseline materialization status

The canonical baseline is `EXPERT-TRAINING-v0.2`; its eight exact source Git blob SHAs are locked in `TRAINING_BASELINE.lock.json`.

During the 2026-10-07 creation of `ios-expert`, the Expert overlay was applied through the GitHub connector rather than by executing `expertctl.py` locally. Therefore the eight source documents were not duplicated into `training/specs/` in the initial migration commit.

This does not change their identity or version: the lock points to immutable blob objects in `lvlaksim1/supervisor`. Before a PP-RM training run, either materialize those exact blobs with SHA verification or read them directly by the locked object IDs. A different text must not be silently substituted under the same baseline name.
