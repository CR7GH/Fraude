# The Wearable Dream — CEO Note

**Question asked:** Can we build a cheap, almost-setup-free wearable that automatically records jump height (dunk sessions, CMJ, squat jump, approach jump), sprint speed, and barbell velocity with eccentric / isometric / concentric timing — with AI agents doing the coding?

**Answer: Yes, it is possible.** Nothing in physics forbids it. Every one of the three measurements has already been achieved by commercial wearables, separately. What nobody has done is put them in one automatic system — and the reasons are engineering and market reasons, not laws of nature. There are, however, four hard limits that no amount of coding will remove. They are listed below, and none of them kills the dream; they only define what the numbers on your screen will mean.

---

## 1. The verdict in numbers

What the beta device can realistically deliver, compared with the laboratory reference and with the best products you could buy today.

| Measurement | Laboratory reference | Best wearable sold today (independent studies) | Our target for the beta | Status |
|---|---|---|---|---|
| Jump height | Force plate (~0.5 cm) | Hip sensor (VERT, Enode): repeatable, but 2–4 cm systematic bias | Repeatability ±1 cm; absolute error ±2 cm after a one-time calibration | **Solid.** Automatic jump detection from a hip sensor is a solved problem (precision ~100%, recall 80–97% in free play). |
| Sprint top speed, outdoors | Radar / laser (~0.05 m/s) | 10 Hz GPS vest (Catapult, STATSports): error 0.12–0.21 m/s | ±0.15 m/s with zero setup | **Solid.** Same technology, cheaper module, plus foot sensor for stride detail. |
| Sprint top speed, indoors | Radar / laser | Nothing good: best foot sensor on the market errs by 0.6 m/s above 7 m/s | ±1–2% (≈0.1–0.2 m/s) after a personal calibration; ±0.1 m/s if two small cones are placed on the lane | **The hardest part.** Doable, but it is the one claim no product has yet proven. |
| Sprint splits (10/20/30 m) | Timing gates (±0.01–0.04 s) | Freelap cones (±0.04 s), needs cones | ±0.05 s without cones, ±0.03 s with two cones | **Good.** |
| Bar velocity (mean concentric) | Cable encoder (GymAware, ±5%) | Bar-mounted sensor (Enode): ±7%; wrist sensors: 10–35% (bad) | ±5–7% (≈0.05 m/s) with the sensor on the bar, not on the body | **Solid**, provided the sensor is on the bar. |
| Eccentric / isometric / concentric timing | Cable encoder | Only the cable encoder publishes it; no cheap sensor is validated for it | ±20–30 ms per phase | **Straightforward physics, unvalidated market** — we will be the ones validating it. |

Everything above assumes the limitations you already accepted (tucking the legs inflates flight-time height, changing lifting form changes bar velocity). Those effects are not errors of the device; they are properties of the measurement, and every product and every jump mat has them.

---

## 2. Why it works — three principles

**Principle 1: time is cheap, position is expensive.**
Jump height does not need to be *measured*; it can be *computed from time in the air*: height = g × t² / 8. A sensor can time take-off and landing to about a millisecond, and one millisecond is worth only 1–2 mm of height. This is why a 30-euro sensor can be as good as a 800-euro jump mat: both do the same calculation. Nobody has to know where you are in space.

**Principle 2: anchor, then integrate briefly.**
An inertial sensor (accelerometer + gyroscope) can reconstruct motion very precisely *for a short time starting from a known state*. If we know the bar is at rest in the rack, we can integrate its motion through one repetition (2–5 s) and get its velocity to a few centimetres per second. If we know the foot is on the ground, we can reconstruct one stride. If we try to integrate for a minute, the errors explode (a tilt error of one degree alone produces a 17 cm/s velocity error per second). The whole design is built around short events with known start and end states: a rep, a stride, a jump. This is the exact opposite of "track everything continuously", and it is why it can be cheap.

**Principle 3: measure the physics first, name it later.**
A flight of 0.6 s followed by an impact is a jump, whatever you call it. A sequence of ground contacts of 0.1 s at 4.5 steps per second is a sprint. A bar that leaves rest, descends, pauses, and rises is a rep. These physical events are detected without any setup and without knowing which exercise you are doing. The *names* (CMJ versus squat jump, back squat versus front squat) are human conventions; the app guesses them from context and asks you to confirm with one tap during the first weeks, after which it has learned your habits. Only one thing can never be guessed: the weight on the bar. You will type the kilograms once per set (one tap to confirm "same as last set").

---

## 3. About the GPS intuition

The intuition "if we had exact (x, y, z) at all times, the algorithms would be easy" is correct in its second half and physically impossible in its first half. The best civilian GPS (RTK, with a correction service and open sky) gives about 1–2 cm horizontally, 2–5 cm vertically, 10–20 times per second, and nothing at all indoors. A 50 cm jump lasts 0.64 s and would be sampled 6 to 12 times with 3–5 cm of vertical noise; a dunk under a roof would not be seen at all. Position from GPS is a map tool, not a jump tool.

But GPS has a second output that people forget: **velocity, measured directly from the Doppler shift of the satellite signals**, accurate to roughly 0.05–0.1 m/s outdoors. That is exactly what the professional sprint vests use, and it is what we will use for outdoor sprints — zero setup, 30–70 euros of module. The deep version of the CEO intuition survives: we do get an "exact trajectory", but it comes from the inertial sensor anchored at known moments (Principle 2), not from satellites.

---

## 4. The four limits that no code can remove

1. **A wearable measures the sensor, not your centre of mass.** Every jump height from a wearable is a proxy: flight-time height tends to read high (+20–35% versus a force plate in published studies), take-off-velocity height tends to read low (−10–18%). These biases are *systematic*, so they are stable and calibratable, and they do not affect progress tracking. But "my vertical is 90 cm" will always mean "90 cm by this method", exactly as it does for a jump mat or a Vertec.
2. **An inertial sensor has no idea how far it has travelled.** Distance and speed need an external reference. Outdoors the satellites provide it for free. Indoors there is none, so the device either uses a personal calibration (you once sprint a tape-measured 30 m) and lives with ~1–2%, or two small beacons are placed on the lane. There is no third way, for anybody.
3. **Mass cannot be sensed by motion.** Kilograms are typed in. (A future force sensor could change this; it is not cheap.)
4. **Labels are human.** The device will know you jumped; it may not know whether you call it a "CMJ" or a "test jump". A one-tap confirmation during the learning period is the price of zero-setup — and it is also the data that makes the pattern recognition personal and reliable.

---

## 5. What the object is

Not one object but a small family of **identical pucks** (roughly 30 × 20 × 10 mm, 10–15 g, a week of battery, rechargeable by USB-C), each containing a motion sensor and a radio. For the beta: two on the shoes (laces), one on a belt at the lower back, one clipped to the barbell. One of them carries a small GPS module for outdoor sprints. The pucks recognise *where they are worn* from the motion itself, so there is nothing to configure: put them on, train, charge them at night. Charging is also when the data is downloaded and processed; results appear in the app.

Why several pucks instead of one? Because the three measurements want three different places: jumps are best timed from the hip and the feet, strides from the feet, and bar velocity from the bar (sensors worn on the body give 10–35% errors on bar velocity in independent tests). Identical hardware keeps the cost and the complexity flat: more pucks are more of the same thing, not a new thing.

---

## 6. Cost, time, and who does what

**Hardware for the beta: about 150–300 euros** in parts (four pucks at 30–50 euros each, plus a 30–70 euro GPS module, straps, a 3D-printed case). Compare with ~1,300–1,500 USD plus yearly subscriptions to buy the three best single-purpose products — which would still not talk to each other or detect anything automatically. No cloud subscription is needed: the processing runs on a laptop or the phone.

**Time: three to six months to a usable beta**, in three stages: (1) pucks assembled and recording reliably; (2) jump and bar velocity validated; (3) sprint and automatic recognition validated, app polished. The device is useful from stage 2.

**What AI agents do:** firmware, the algorithms, the app, the data pipeline, the validation analysis, the documentation. This is ordinary engineering with a large published literature behind it.

**What a human must do:** solder and assemble the pucks, wear them, do the ground-truth sessions (filming jumps, lifts and sprints with a phone at 240 frames per second, plus one tape-measured sprint), and press the confirmation taps in the first weeks. The device cannot be validated from a desk. This is the one "pitfall AI cannot overcome": the data must come from a body in a gym.

**How we will know it works:** every claim in the table of section 1 will be checked against phone video, which is itself a validated reference (video flight time agrees with force plates to about 1 cm; video sprint times agree with timing gates to 0.01 s; a 45 cm Olympic plate in the frame gives bar velocity to ~0.01 m/s). Nothing needs to be rented from a laboratory, although one force-plate session would be a nice extra.

---

## 7. Risks worth knowing about

- **Indoor sprint speed** may land at 2% rather than 1%. Mitigation: the two-cone option (an extra 30–50 euros) brings it to 0.1 m/s.
- **Foot sensors are abused**: sprint landings exceed 50 g and spin the foot faster than cheap gyroscopes can follow. Mitigation: a second high-range accelerometer in the shoe pucks (10 euros) and 1,000 samples per second.
- **Automatic recognition is only as good as the first weeks of confirmations.** This is learning, not magic; with one user it becomes very reliable, and generalising to other users later will need other users' data.
- **Deep squats** are where bar-mounted sensors have the worst published errors (large systematic overestimates). Mitigation: our per-rep resets plus the fact that a squat ends where it starts (a second constraint the cheap products do not use); we will measure how far it gets us.

---

## 8. After the beta

If the beta validates, production is a custom circuit board with a pre-certified radio module (no radio certification of our own), a moulded case, and an app port to the phone. Unit cost at a few hundred units is roughly 25–40 euros per puck; a four-puck kit could sell well under the price of a single existing single-purpose device. The regulatory burden for a non-medical sports sensor is light (CE/FCC via the certified module, battery safety). The genuinely new value — and the defensible one — is not the sensor; it is the automatic, multi-activity, validated pipeline that nobody has shipped.

**Decision requested:** approve a 150–300 euro beta build and the time of one tester for three to six months. The technical note (`docs/TECHNICAL_NOTE_wearable_dream.md`) specifies the build in full.
