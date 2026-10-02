# measurement/raw/

Empty. No measurements exist — no hardware exists.

## APPEND-ONLY

Files in this directory are written once and **never edited, never overwritten, never deleted.**

Raw measured data is the only artefact in this project that cannot be regenerated. A simulation
can be re-run. A measurement can be repeated only while the board still exists, still works, the
instrument is still available, and the same calibration is still valid.

If a measurement is wrong, take another one and give it a new filename. Keep the wrong one — a
measurement that turned out to be bad is itself evidence, and the reason it was bad is usually
worth recording.

**Naming:** `YYYY-MM-DD_<DUT-or-coupon>_<cal-method>_<repeat-number>.s2p`

Every file needs a row in the measurement log in `../measurement_plan.md`.
