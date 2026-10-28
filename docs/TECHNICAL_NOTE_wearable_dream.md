# Technical Note — Automatic wearable measurement of jump height, sprint speed and bar velocity

Companion to `CEO_NOTE_wearable_dream.md`. Scope: first-principles feasibility, design, error budgets, build plan and validation for a one-person, multi-month beta; cheapest viable hardware.

## 0. Summary and targets

| Quantity | Primary estimator | Node(s) | Beta target | Evidence it is reachable |
|---|---|---|---|---|
| Jump height (all jump types) | Flight time h = g·t²/8, take-off from hip free-fall onset, landing from first foot impact | Hip + 2 shoes | Test–retest SD ≤ 1 cm; bias ≤ 2 cm vs video after calibration | Output V2 vs Kistler force plate: r ≥ 0.983, CV ≤ 2.3% (2025); custom 1 kHz L5 IMU: 97.4% detection, flight-time bias −11.7 ms (Sensors 2026) |
| Take-off velocity height (CMJ/SJ only) | h = v0²/2g from hip integration from quiet stance | Hip | Secondary metric, reported alongside | Mohammadian 2024: take-off-velocity method −10–18%, flight-time +22–35% vs FP; biases systematic |
| Sprint top speed outdoors | GNSS Doppler velocity 10–25 Hz fused with foot strides | Back/hip GNSS + shoes | ±0.15 m/s | 10 Hz GNSS vs laser: RMSE 0.12–0.21 m/s (Crang 2024) |
| Sprint top speed indoors | Foot ZUPT stride integration + personal scale calibration (+ optional 2 UWB/magnetic cones) | Shoes (+ cones) | ±1–2% calibrated; ±0.1 m/s with cones | 1125 Hz ±200 g foot IMU ZUPT at 6–9.3 m/s: stride bias −0.27% (LoA ±4.6%), 0–70 m distance bias −1.1% (LoA ±3.5%) (PLoS One 2024) |
| Splits 10/20/30 m | Distance from fused trajectory, start = first movement | Shoes (+GNSS/cones) | ±0.05 s (±0.03 s with cones) | Photocell class MAE ≤ 0.04 s; 0.3 m distance error = 35 ms at 9 m/s |
| Contact / flight time per step | Shoe impact and toe-off at 1 kHz | Shoes | ±5 ms | Body-IMU biases 10–40 ms published; foot sensor is the fix |
| Bar mean concentric velocity (MCV), peak, MPV | Bar-mounted IMU, per-rep rest resets, ROM closure | Bar | ±0.05 m/s (≈5–7%) | Enode SEE 7% (0.08 m/s), GymAware LPT 5.4% (Fritschi 2021); 2 Movesense on bar: MAE 0.03–0.06 m/s < 1.3 m/s (KTH V-LO) |
| Phase durations (ecc/iso/conc) | Velocity sign and threshold crossings | Bar | ±20–30 ms | Zero-crossing timing; unvalidated commercially — validated by us vs 240 fps video |

## 1. Physics and sensitivities (computed)

- Flight time: h = g t²/8 → dh/dt = g t/4. For 30–100 cm jumps t = 0.50–0.90 s, dh/dt = 1.2–2.2 m/s. **1 ms timing error = 1–2 mm; 10 ms = 1.2–2.2 cm.** Sample rate is not the limiting term; the physical definition of take-off/landing instants is.
- Take-off velocity: h = v0²/2g → dh/dv0 = v0/g. 0.05 m/s error on v0 = 1.4–2.0 cm.
- Gravity leakage of an attitude error ε over integration time T: Δv = g sin ε · T. 1° over 1 s = 17 cm/s; 0.25° over 0.5 s = 2 cm/s; 1° over 2 s = 34 cm/s. **Conclusion: integrate only over short events that start from a known state (ZUPT), and only on rigid mounts (bar) expect attitude ≤ 0.3°; on soft tissue (hip) prefer timing-based estimators.**
- Accelerometer bias 1 mg: Δv = 1 cm/s per second of integration — secondary for events < 3 s.
- Barometer: dynamic pressure ½ρv² = 5.4 Pa at 3 m/s = 46 cm of fake altitude (dp/dz = 11.8 Pa/m). **Useless for jumps or sprints; excluded.**
- GNSS position: RTK 1–2 cm horizontal, 2–5 cm vertical, 10–20 Hz, outdoor only. Not a jump sensor. GNSS Doppler velocity 0.05–0.1 m/s: a good speed sensor outdoors.
- UWB single anchor: range noise 5–10 cm at 100 Hz, linear fit over 0.5 s → radial speed std 0.05–0.10 m/s.
- Sprint: step length 1.8–2.4 m at 8–11 m/s; 1–2% step error = 0.1–0.2 m/s.

## 2. Measurement design

### 2.1 Jump height
Estimators:
1. **Flight time (primary, all jump types).** Take-off = onset of hip free fall (|a_specific| falls below ~0.2–0.3 g and stays there ≥ 150 ms); landing = first impact spike on either shoe node (> 5 g, rising edge at 1 kHz). Using the hip for take-off and the feet for landing fixes the two known biases: hip-only landing is late by 10–30 ms (shock transmission) which explains VERT-type overestimation; foot-only take-off is early on one-foot jumps (free foot leaves first).
2. **Take-off velocity (CMJ, SJ from quiet stance).** Hip node: attitude from gravity during the quiet 1 s before movement, gyro propagation through the jump, integrate vertical specific force from movement onset to take-off; h = v0²/2g. Report both; the pair also flags landing-posture effects (flight-time ≫ v0-based = legs tucked).
3. Jump typing: run-up present (foot stance cycles > 2 m/s before take-off) → approach jump; one vs two-foot take-off from the gap between each shoe's last contact and the hip free-fall onset; CMJ vs SJ from presence of a countermovement (hip unweighting phase).
Error budget (flight time): take-off ambiguity ±5 ms, landing ±2 ms, timestamp sync ±1 ms → ±1.5 cm worst case, ≤ 1 cm typical. Systematic: method bias vs force plate (calibrate once with the video protocol in §7).
Fundamental: sensor ≠ centre of mass; posture at landing. Engineering: edge definitions, soft-tissue motion, saturation.

### 2.2 Sprint speed
1. **Shoe nodes, 1 kHz, ±32 g (+ ±200 g secondary accelerometer), ±4000 dps gyro.** Stance detection from impact + minimum angular-rate instant; ZUPT applied at the sagittal angular-velocity zero crossing (brief, ~5–10 ms at top speed, hence 1 kHz). Contact-point constraint (sensor velocity = ω × r, r ≈ 7 cm known) instead of naive v = 0. Integrate per stride with gravity from the gyro-propagated attitude; close each stride with the velocity boundary condition and distribute drift linearly. Published result for this class of hardware: 0–70 m distance −1.1% bias, LoA ±3.5%.
2. **Personal scale calibration**: 3 maximal runs over a tape-measured 30–40 m; fit one scale factor per shoe. Expected residual ≤ 1–2%.
3. **GNSS Doppler (outdoor)**: u-blox NEO-M9N class module (25 Hz) on a back/hip node, patch antenna skyward. Fuse in a Kalman filter: GNSS supplies absolute scale, feet supply within-stride profile and splits. Expected top-speed error ±0.15 m/s.
4. **Indoor option**: two UWB modules (DW3000 class) or magnetic beacons at 0 and 30 m; two-way ranging to the hip node at 100 Hz → ±0.05–0.1 m/s and gate-grade splits (±0.03 s).
Sprint detection: ≥ 6 consecutive stance cycles with stride speed > 6 m/s; drills/jogs excluded by speed and contact time.
Fundamental: no inertial absolute reference; indoors needs calibration or placed equipment. Engineering: saturation, ZUPT instant definition, antenna shadowing.

### 2.3 Bar velocity and phases
1. **Bar node strapped to the shaft** (inside the collar; magnet on the sleeve end cap acceptable only with spin compensation ω²r). Body-worn sensors are excluded for bar velocity (Beast wrist CV 35%, PUSH 9–11% vs LPT 2.6–5%).
2. Rest detection: |a| = 1 g ± 0.05 g and |ω| < 5°/s for ≥ 300 ms → zero-velocity reset and attitude re-initialisation from gravity (≤ 0.2° on a rigid mount).
3. Per rep: rotate specific force to world frame, subtract g, integrate v(t); enforce v = 0 at both rests; for squat/bench also enforce position closure (same height at start and end). Metrics: MCV, MPV (concentric until a < −g), peak velocity, ROM, eccentric/isometric/concentric durations (thresholds |v| < 0.05 m/s for ≥ 100 ms = isometric; sign gives ecc/conc; deadlift begins concentric), velocity loss across the set.
4. Expected: ±0.05 m/s MCV; worst case in deep squats (Enode MAPE 10–42% published) — the position-closure constraint is our mitigation and will be measured.
5. Exercise recognition: hip node orientation (lying = bench), bar rest height relative to hip (barometric differential is not reliable; use ROM and bar path signatures instead), one-tap confirmation; load in kg entered per set with "same as last" default.
Fundamental: mass unobservable from kinematics; form changes change velocity (accepted). Engineering: drift, spin, vibration.

## 3. System architecture

- **Nodes (identical)**: nRF52840 (Seeed XIAO nRF52840 class, BLE 5, USB-C, LiPo charger) + IMU LSM6DSO32 (±32 g, ±2000 dps) or LSM6DSV16X (±16 g, ±4000 dps); shoe nodes add ADXL375 (±200 g); 128 MB SPI NOR flash (W25Q01JV) or microSD; 300–500 mAh LiPo (≈ 30 h active at 10–15 mA; weeks in motion-triggered sleep); 3D-printed case; lace clip, lumbar elastic belt, bar strap.
- **GNSS add-on** on the hip/back node: NEO-M9N breakout (30–70 €), 25 Hz, Doppler velocity output.
- **Optional indoor cones**: 2 × DWM3000 modules (≈ 20–30 € each).
- Sampling: shoes 1000 Hz, hip 500 Hz, bar 400 Hz. Data rates 5–14 kB/s per node; full-session raw logging to flash (≈ 50 MB/h at 1 kHz); BLE used for live event summaries only (jump height within 1 s of landing) and for small event windows; bulk download via USB mass storage at charging time.
- Time sync: BLE connection-event timestamps + hourly sync beacons → ≤ 1 ms across nodes (needed only for hip-takeoff/foot-landing pairing and one-foot/two-foot typing).
- Firmware: Zephyr (nRF Connect SDK), IMU FIFO over SPI, flash logger, event detectors (§4), BLE GATT service for events, USB MSC.
- Processing: Python pipeline (numpy/scipy) on laptop for the beta (ingest, calibration, estimators, fusion, reports, validation statistics); phone app (Flutter) shows sessions and asks confirmations; later port the estimators to the phone.
- Cost: 4 nodes 120–200 €, GNSS 30–70 €, straps/case 20 €, cones optional 50 €. Total 150–300 €.

## 4. Automatic recognition pipeline (near-zero setup)

1. **Node self-location** from motion signatures over the first minute of wear: shoe (periodic stance/ZUPT pattern with impacts), hip (1 g vertical at rest, walking oscillation 2–3 Hz without impacts > 5 g), bar (long rests at 1 g, vertical-only motion, no walking), pocket/idle (random). Accuracy expected > 99% after a few sessions; manual override in app.
2. **Physics-first event extraction** independent of labels: flight phases (free-fall windows > 250 ms), stance cycles (contacts, speed per stride), lift reps (rest → motion → rest with monotonic phases). Every event gets its physical metrics regardless of naming.
3. **Context labelling**: session type from the mix of events and nodes present; exercise names from a lightweight classifier (gradient-boosted trees on event features) seeded by one-tap confirmations; "same as yesterday" defaults; corrections re-train nightly. Expected after 4–6 weeks for one user: > 97% event recall/precision, > 95% label accuracy; remaining errors are visible as mislabelled sets the user can fix in two taps.
4. **Load entry**: per set, one tap to confirm the proposed kg (last set / planned progression). This is the only unavoidable manual input.

## 5. Calibration (once, at setup)

- IMU: 6-position accelerometer bias/scale and gyro bias at room temperature; re-estimated opportunistically at every rest.
- Jump: 10 CMJs filmed at 240 fps → per-user method offset vs video flight time (expect |bias| ≤ 1–2 cm after offset).
- Sprint: 3 runs over a tape-measured 30–40 m → stride scale factor per shoe; outdoor GNSS cross-check.
- Bar: 10 reps each of squat/bench/deadlift filmed at 240 fps with a 450 mm plate in frame → scale check and threshold tuning.

## 6. Build plan (3–6 months, one tester)

1. Month 1: assemble 4 nodes, firmware logging at full rate, USB download, Python ingest, self-location, event extraction on raw data. Deliverable: raw sessions and plots.
2. Month 2: jump and bar estimators + video validation; app v0 (sessions, results, confirmations). Deliverable: validated jump and VBT numbers.
3. Month 3: sprint (foot ZUPT, GNSS fusion, calibration), indoor cone option; validation. Deliverable: validated speed and splits.
4. Months 4–6: automatic recognition, nightly learning, robustness (drops, battery, detachment), continuous use, decision data for production.
AI agents build everything in software and the analysis; the human assembles, wears, films, confirms.

## 7. Validation protocol (phone only)

- **Jump**: 240 fps video from the side; frame-count flight time (±1 frame = 4.2 ms ≈ 7 mm). Video flight time agrees with force plates to ~1 cm (My Jump 2: ICC 0.997, bias −1.2 cm). 30 jumps per type; report bias, LoA, ICC, test–retest SD. Pass: SD ≤ 1 cm, |bias| ≤ 2 cm after offset.
- **Sprint**: phone perpendicular to a tape-measured 10 m "flying" segment at 240 fps → segment time ±4 ms ≈ ±0.04 m/s; plus 30 m splits from 60 fps start/finish framing (MySprint-class video gives SEE 0.007–0.015 s vs gates). 10 runs outdoor, 10 indoor. Pass: top speed ±0.15 m/s outdoor, ±2% indoor (±0.1 m/s with cones), splits ±0.05 s, contact time ±5 ms.
- **Bar**: 240 fps side video, 450 mm plate as scale, automatic plate tracking → position ±2 mm → MCV ±0.01–0.02 m/s. 10 reps × 3 lifts × 3 loads. Pass: MCV ±0.05 m/s, phase durations ±30 ms, rep detection ≥ 99%.
- **Recognition**: weekly confusion matrix from confirmations; pass: > 97% event recall/precision and > 95% labels by week 6.

## 8. Fundamental vs engineering limits (why-chains)

1. *Why can't the jump height match a force plate exactly?* Because the wearable measures flight time, not take-off impulse. *Why not impulse?* Because the hip sensor is not the centre of mass and its attitude on soft tissue is uncertain by ~1°, which leaks 17 cm/s per second. *Why not fix attitude?* Because no body-worn sensor is rigidly attached and the leg/arm segments move relative to the pelvis in flight. *Why not add sensors?* Because more segments only approximate the centre of mass; the force plate measures it directly. **Fundamental; mitigated by calibration and consistent methodology.**
2. *Why can't indoor sprint speed be radar-grade?* Because inertial sensors integrate acceleration and need a reference to bound errors. *Why isn't the foot ZUPT enough?* Because at top speed the foot is never still for more than milliseconds and pivots on the forefoot, so the "zero" is a modelled velocity, not a measured one. *Why not model it perfectly?* Because shoe compliance, slip and forefoot rolling vary per step. *Why not another sensor?* Barometers fail from airflow, optical flow saturates above ~1 m/s at shoe height, Doppler radar on a body with legs in the beam is unproven. **Fundamental for a sensor-only indoor solution at < 1%; engineering at 1–2%; solved with two cones.**
3. Mass: unobservable from kinematics → entered. Labels: conventions → confirmations. GNSS vertical: multipath and geometry → not a jump sensor.

## 9. Risk register

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Shoe sensor saturation (impacts > 32 g, foot > 2000 dps) | High | Sprint speed, contact time | Dual accelerometer (±200 g), ±4000 dps gyro, 1 kHz, ZUPT instant chosen outside impact |
| ZUPT instant ill-defined at top speed | High | Indoor speed 2–4% | Contact-point constraint, personal calibration, GNSS outdoors, cones indoors |
| Deep-squat bar velocity overestimation | Medium | MCV error > 0.05 m/s | Position-closure constraint, rest resets, validate per lift |
| Hip take-off detection on one-foot approach jumps | Medium | ±2 cm | Hip + both feet fusion, video tuning |
| BLE drops / data loss | Medium | Missing sessions | Flash logging first, BLE second, USB bulk download |
| Sensor detachment / sweat | Medium | Bad sessions | Lace clip + tether, IP54 case, detachment detector |
| Label errors in automatic recognition | Medium | Wrong exercise names | Confirmations, nightly retraining, easy fix in app |
| One-subject overfitting | Certain for production | Generalisation | Keep physics-first estimators user-independent; only labels are personal |
| Battery/charging routine | Low | Missed sessions | Motion-triggered sleep, charge dock = sync |
| GNSS shadowing by body | Medium | Outdoor speed | Upper-back placement, Doppler quality gating, foot fallback |

## 10. Production path

Custom PCB with a pre-certified BLE module (Raytac/u-blox/Fanstel class) → no radio certification of our own; CE/FCC/RED via module and battery safety; moulded case; phone-side estimators; unit cost ≈ 25–40 € per puck at a few hundred units. Validation with more subjects (recognition labels) is the main cost before a launch.

## 11. References (key)

Charlton 2017 J Sci Med Sport (VERT vs mocap); MacDonald 2017 Phys Ther Sport; Mohammadian 2024 J Biomech (method bias); Output V2 vs Kistler, SAGE 2025 (DOI 10.1177/17543371251395819); Pousibet-Garrido 2026 Sensors 26(5):1408; Balsalobre-Fernández 2015 (My Jump 2); McMahon 2016 (Just Jump); Glatthorn 2011 (Optojump); Crang 2024 J Sci Med Sport (GNSS vs laser); Myhill 2023 Sci Med Football (Playermaker); PLoS One 2024 PMC10852269 (sprint ZUPT); Sensors 2022 (shoe IMU 35 m sprints); photocell review 2024 PMC11079923; Romero-Franco 2017 EJSS (MySprint); Fritschi 2021 Sports (VBT devices vs mocap); Pérez-Castilla 2019 JSCR (seven VBT devices); Behrmann 2025 Sensors 25:549 (Enode squat); Weakley 2021 Sports Med (VBT review); KTH V-LO open-source project; Sports 2023 PMC10383699 (Apple Watch on bar).
