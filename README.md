# blazar-video calibrations

The calibration data contract between the Python `calibrator` and the Rust
`blazar` runtime. A calibration answers "how should this content be encoded?"
for one point in the key space `(model_identity × scene × codec × target)`.

Format spec: `calibration-format.md` (kept outside git for now).

## Layout

- `default/` — the opinion-free, codec-stock default calibrations that ship with
  Blazar. These are the measurement **control group**: no generative tuning baked
  in, so tuned calibrations can be measured against them. One per `(codec, target)`.

Tuned calibrations (produced by the calibrator) and user-authored calibrations
insert at higher specificity above these defaults. On-disk layout is NOT
semantically meaningful — the resolution key lives inside each file.

## Source tiers

Each calibration declares `source = default | calibrator | user`. Resolution is
specificity-ordered; `source` only breaks ties at equal specificity
(`user > calibrator > default`), and the tie-break is logged.

## License

Apache-2.0. See `LICENSE`.
