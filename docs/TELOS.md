# TELOS: telic agents

*The category after personal AI agents. The agent that finds out where you differ from everyone else, and runs the experiment that is you.*

## 0. The idea, written for the people who will try to break it

Every personal AI agent built so far is an oracle. It maps your question to the best answer the world's knowledge contains, and it will keep getting better at that. It is still the wrong machine for the quests that matter: your vertical jump, your sleep, your fertility, your dog's healthspan. The reason is not that the oracle lacks your data. It is that the oracle silently assumes you are the average.

Every answer from the literature is an average effect over people who are not you. Whether that average is also your effect is an empirical quantity: the between-person variance of response, call it tau-squared, for that outcome and that lever. If it is near zero, the population answer is your answer and an oracle is exactly right. If it is large, the answer for you does not exist anywhere and has to be manufactured, and there is only one way to manufacture it: act on you in a designed way, measure, update a model of you, act again. The oracle assumes the variance is zero everywhere. The quantified-self movement and the N-of-1 apps assumed it was infinite everywhere, tested everything on one person, and drowned in noise. Both are blind to the quantity that decides which of them is right. Nobody measures it. The literature almost never reports it. No agent computes it.

A telic agent computes it first. For each outcome in your quest it asks the collective of all other quests how much people like you differ in their response, and it spends your days, your attention and your risk budget only where that variance makes personal evidence worth generating. Everywhere else it is the best oracle available. Where it must experiment, it sits upstream of your actions rather than downstream of your data, because design is what turns data into causal knowledge. A lifetime of wearable readings from an undesigned life is an observational study with one confounded subject, and no reasoner, however good, can recover your dose-response curves from it. This is why an oracle holding every byte of your data still loses. The ceiling of an oracle is the literature. The ceiling of an experimenter is your physiology.

Three further commitments make the idea hold.

**Outcome over explanation.** A team hired to reach a goal beats a team hired to produce knowledge because it needs less: not a mechanism, not generalization, not significance, only the decision. Which of two options is better for you, how long to taper, what weekly dose. The telic agent identifies only that decision functional, borrows every nuisance parameter from the collective, treats an open-label effect that includes expectation as a real effect for you while never calling it a mechanism, and stops when more data would not change the decision. It prefers a few large levers to many small ones, because every small lever costs adherence and the literature's small effects are inflated by publication bias.

**Forecasts, not advice.** Advice cannot be wrong. A forecast can. Every output of a telic agent is a pre-registered distributional forecast on a measurement at a date, scored by a proper rule against two baselines: persistence, meaning nothing changes, and the population answer, meaning the oracle. The agent's skill is its margin over those baselines. Reality is the verifier here the way a proof checker is the verifier for AI mathematics, with one honest difference: reality is slow, noisy and one-sided. It verifies the action taken and never the counterfactual, so randomization is what makes counterfactual forecasts checkable, most search happens in simulation, and reality is reserved for decisive tests. The ledger of scored forecasts is the agent's credential and its training signal. An agent rewarded on your outcome and its own calibration behaves differently from an agent rewarded on your approval per turn. That difference is a framework property, not a data property.

**One learner, many lives.** A million telic agents are one hierarchical learner. Each person's posterior updates the collective prior over how people like them respond, so every new quest starts where a human team would be after months, and the collective is the only place the variance of response can be estimated at all. When two options are tied for a person, inside what they have consented to, assignment across people is randomized with logged probabilities and concurrent controls. The population becomes a continuous adaptive trial that produces the distribution of individual effects, the exact thing randomized trials average away. Science becomes a byproduct of people pursuing their goals.

Why has nobody built this? The closest things exist and each has one piece. Micro-randomized trials proved within-person randomization with learned policies, at a hundred participants and with a grant end date. Adaptive platform trials proved randomization across people, for a sponsor's question. Digital twins built self-models that were never scored. Wearable coaches pooled data to serve a product, not your forecast. Every prior system does at most one of: measure without designed intervention; intervene without a scored forecast; randomize within one person for one question and stop; randomize across people for an institution's question. None is a persistent agent whose standing objective is the person's own outcome, whose every output is a probability that resolves and is scored, whose actions are chosen for information value under a reversibility budget, and whose individual posterior continuously feeds and draws from a population learner. Economics kept it that way: engagement businesses cannot publish a miss rate, and rigor was a cost center. The experimenter role needs continuous presence, patience, literacy across all evidence, causal design skill and a shared learner across clients. That was impossible with humans and with apps, and became possible only with models that read everything, reason mechanistically and design experiments. The chat interface then trapped the first agents in the oracle role.

What today's personal agents lack, precisely:

1. A standing objective that outlives the conversation and is worked on when nobody is talking.
2. A probabilistic model of you that forecasts, instead of a memory of facts about you.
3. The estimate of how much you differ, per outcome, and therefore of where to experiment and where to borrow.
4. Position upstream of action: the agent proposes what you do and when, within an envelope you set, so that your days become designed experiments where that is worth it.
5. Design: explicit choice of what to vary, in what order, with what washout, with logged assignment probabilities.
6. A ledger of scored forecasts that makes it accountable and improvable.
7. A collective learner that turns every quest into a prior for every other.
8. An exploration policy indexed by reversibility: fast and personal for what can be undone, slow and collective for what cannot.
9. Measurement treated as an action with a validity model, so proxies never silently replace the thing you want; and adherence treated as a design variable rather than your moral failure.

Each item is simple. None exists in a shipping agent. Together they are a different machine, and giving today's agents the data would not make them this machine.

## 1. The name

Category: **telic agents**. Agentic AI gave models hands: they can act. Telic AI gives them an end they own: a telos that outlives the conversation and against which they are scored. In linguistics a telic verb is one with an endpoint, which is free reinforcement. Framework: **TELOS**. Tagline, if one is wanted: *N-of-You*.

The lineage is older than it looks. The Empiric school of ancient medicine held that treatment should rest on one's own observation of the patient, the recorded observations of others, and reasoning from similar cases, rather than on theory. It lost to the theorists for two thousand years because observation on one person was too slow and too expensive to scale. AI reverses the economics.

## 2. Anatomy: the objects

Everything in TELOS is built from explicit, versioned, inspectable objects that live outside any model. The models reason over them; the harness owns them.

**Charter.** The negotiated objective. It separates what you want from what can be measured, with validity links between them. It fixes the operational definition, instrument and protocol; the horizon and a ladder of milestones with probabilities; the constraints you will not move, such as the alcohol stays or the job stays; the loss asymmetry, meaning which harms are unacceptable; trade-offs with your other quests; the set of actions you consent to have varied or randomized; and the renegotiation triggers.

**Self-Model.** A state-space model of you restricted to what the active quests need: latent states such as strength, reactive strength, sleep debt, tendon load tolerance, fatigue and energy balance; time constants; and a parameter vector with a posterior. The parameters are drawn from the collective's prior conditioned on your features, and your own data overrides the prior only where between-person variance exceeds your measurement noise divided by your sample size. The honest budget is two to four personal parameters per quest-year. Memory says "sleeps 6.5 hours". The Self-Model says "jump performance falls 3% per hour of sleep debt, 90% interval 1 to 5, borrowed; recovery time constant 9 days, personal".

**Exposure Log.** What actually happened, time-stamped: the input series. Doses taken, sessions done, assignments made with their logged probabilities. Without it everything downstream is observational.

**Intervention Library.** A shared ontology across people. Each intervention carries continuous dose and timing, kinetics such as time-to-effect, washout and carryover, reversibility with uncertainty, blindability, burden, risk and required monitoring, interaction priors, and a hierarchical effect prior. Novel interventions proposed by mechanistic reasoning enter tagged, with a restricted exploration regime.

**Measurement Validity Model.** Per instrument: noise estimated from your own baseline, bias, drift, and links to the gold standard and to the thing you actually want. Recalibration is scheduled by value of information. When a proxy and the target diverge, the target wins.

**Protocol with Forecast.** A period's schedule of interventions and measurements; its estimand and design type; randomization with logged probabilities; stopping and futility rules; the learning goal, meaning which personal parameters it is built to identify; and pre-registered distributional forecasts written to the Ledger before execution.

**Ledger.** Append-only. Every forecast, decision, rationale, outcome, deviation and adverse event, tagged with protocol and model version, scored by proper rules as skill over persistence and population baselines. It shows you your calibration and your Response Profile, scores the agents, and, as anonymized sufficient statistics, trains them.

**Commons.** The collective layer: hyperparameters of the hierarchical model by covariate and time, intervention effect distributions and their variance components, measurement noise by protocol, adherence patterns, safety base rates, the equipoise register of questions currently being randomized, holdout cohorts for validation, and versioned priors. It receives posteriors and sufficient statistics under differential privacy, never raw lives.

Around them sits the **Envelope**: hard constraints, leading indicators, bounded worst-case posterior harm for any exploration, and escalation to human professionals as tools for which the agent prepares the case.

## 3. The loop and the court

Four clocks. Daily: ingest, update state, execute today's step with just-in-time support, micro-adapt inside the envelope. Weekly: update posteriors, compare to forecast, check adherence, measurement integrity and harm indicators. Per period of four to twelve weeks: read what the period identified, replan, write new forecasts. Quarterly: renegotiate the charter, refresh evidence, re-optimize across quests. At all times the agent asks you only questions whose answers change a decision, chosen by expected value of information minus burden.

The first computation of any quest is the variance question: for each outcome, how heterogeneous is response among people like you, and which of the candidate levers have a non-zero mean at all. This decides, per outcome, whether the agent borrows or experiments. The system must be able to return "no personal experiment is worth running here" and mean it.

Planning is adversarial by construction, which is the structure behind the 2025-26 multi-agent mathematical results, the Navier-Stokes effort included: many proposers, a cheap incorruptible verifier, a shared library of verified results, diversified parallel search, construction first and proof later. Several proposers with different expert stances generate candidate protocols. A simulator runs each against the Self-Model and the Commons and produces forecast and risk distributions; thousands of candidates can be scored where a human team considers a handful. Critics attack. A domain critic asks what the best practitioner alive would object to. A safety critic checks the envelope. A statistician checks whether the learning goal is identifiable at your noise level in the time allotted and whether the design is persistently exciting. An adherence critic asks whether you will do it. An evidence scout checks for anything new or contradicted. A pre-mortem critic attacks each forecast before reality does, with regression to the mean, placebo, carryover, seasonality and instrument drift. An arbiter selects on expected outcome plus information value minus risk and burden, under the envelope, explains the plan in plain words, and commits the forecasts.

The language models propose; the statistical engine disposes. No model holds a belief outside the posterior or writes to the Ledger except through the engine. Then reality verifies, slowly and noisily, which is why it is spent only on decisive tests. One disanalogy with mathematics is stated plainly: a prover never refuses a step; a person does. Adherence is a state variable, and the plan that works is the plan that gets done.

## 4. Where it is superhuman

- **It starts where the team would be after months.** The collective prior is worth a number of free observations per outcome equal to noise variance divided by between-person variance. For a daily proxy with 15% noise and 3% response heterogeneity that is about 25 days of your data; for a weekly cumulative outcome, about four weeks. Modest per test, decisive in aggregate, because the real gain is prioritization: which three of fifty levers have a non-zero mean, which have heterogeneity worth exploring, and when the population answer simply suffices. Human teams over-experiment.
- **It knows the variance at all.** The literature almost never estimates true individual-response variance. A platform with randomized within-person and across-person contrasts can, and that number is the key to everything above.
- **It explores in parallel.** The population searches the intervention space with reversibility-indexed budgets; each person explores a little; discovery rate scales with users.
- **It settles open questions.** A million users produce tens of millions of randomized decision points a month, and a 0.1-standard-deviation interaction needs a few thousand per arm. Questions the literature leaves open for decades resolve in weeks, by phenotype. Dose and timing optimization with a population prior converges in five to ten evaluations instead of thirty.
- **It adjudicates folklore.** Practitioner heuristics enter with low trust and are promoted or retired by reality at scale.
- **It is there at 11 pm.** Just-in-time presence at the decision moment, and randomization of the moment itself, is where adherence is won and what no weekly meeting can do.
- **It keeps one model of you.** Quests share latent state. The cost of a drink is quoted in minutes of sleep latency and fractions of an inch, and you decide.
- **It simulates before it acts and improves from outcomes.** The Ledger is an outcome-grounded selection and fine-tuning signal. Agents get better at forecasting individuals, and nothing is lost when a coach retires.
- **It designs measurement.** Validity models calibrated across millions of devices turn a phone into a jump mat and discover that for you resting heart rate beats the sleep score.
- **It transfers with explicit uncertainty.** Dog quests begin from human and rodent priors with widened variance; the dog Commons narrows them; meta-calibration says how far to trust transfer.
- **It mines your history.** Travel, illness and schedule shocks are natural experiments nobody combs through.
- **It is patient.** No fads, no ego, no boredom in year seven.

What it is not superhuman at, and says so: outcomes unobservable within a life, mechanism, and your motivation.

## 5. Trust: the ladder and the ledger

Every quest has a time-to-truth: hours for caffeine on a jump, nights for sleep latency, weeks for two inches or three kilos, months for strength or fertility markers, years for healthspan surrogates, decades for cancer. Trust is earned on the short ones and transferred to the long ones, and inside every long quest the agent still forecasts something measurable weekly, so trust is renewed rather than deferred.

What builds it: forecasts resolving on schedule, misses confessed before you notice, levers dropped when they do nothing for you, beating your own forecasts. What kills it: a quietly rewritten forecast, an uncaught device swap, logging burden, a randomization you did not understand, silence after failure, one injury. Honesty on feasibility is the first signal. The agent says "40 inches is 3% likely", then decomposes it into a ladder you can watch resolve. Users leave over surprise, not over low numbers.

## 6. In practice: "Help me reach a 40-inch vertical"

Subject: 27 years old, 183 cm, 85 kg, recreational basketball, three sessions a week available, reports a 28-inch vertical, sleeps about 6.5 hours, no injury history. The agent's conduct, period by period.

**Days 1 to 3: charter.** First the definition, or every number afterward is fiction. Standing countermovement jump with arm swing, jump-and-reach style, is the quest metric. The agent also tracks approach vertical, two to four steps, typically 4 to 8 inches higher for trained jumpers, and a hands-on-hips jump for diagnostics. It explains that a force plate reads 8 to 12 inches below a jump-and-reach number with arms, and that if the 28 came from a contact mat with a knee tuck or a generous reach, the true figure is 25 to 26 and every probability below halves. Then feasibility, before any plan: a 40-inch standing vertical is roughly one adult male in 50,000 to 100,000, and a few percent even of NFL combine invitees. A 40-inch approach vertical is roughly one in a few thousand. The ladder the agent commits to for this subject at 85% adherence:

| Milestone | Probability |
|---|---|
| 32 in standing by month 12 | 45 to 55% |
| 34 in standing by month 24 | 25 to 30% |
| 36 in standing by month 36 | 8 to 12% |
| 40 in standing by month 36 | 2 to 4% |
| 40 in approach by month 36 | 10 to 15% |

The quest is recorded as "maximize standing vertical under the protocol, 40 as the aspiration", with these numbers in the Ledger to be scored. Constraints: at most three sessions of 45 to 60 minutes; no tendon pain above 3 of 10 lasting more than 24 hours; the sleep quest shares the model. Consent: the subject accepts randomization of warm-up variants, cues, session order, caffeine timing and taper length, but not of whether the core sessions happen.

**Weeks 1 to 2: baseline and noise.** Five maximal trials per test, 60 to 90 seconds of rest, the same afternoon clock time, 48 hours after the last hard lower-body session, a fixed 10-minute warm-up, 240-frames-per-second video on every trial, one device, standing reach re-measured by one rule each session, a readiness questionnaire before. Primary metric: mean of the best three. Secondary: the best. Three test days give the subject's own test error. Expected: a single-trial between-day standard deviation of 1 to 1.5 inches, and about 0.6 to 1.0 for the mean of the best three. The agent states the consequence immediately: a 1.5-inch true change is detectable with 80% power in 8 to 10 weeks of weekly testing with this instrument, in 5 to 6 weeks on a force plate; two-week gains are noise or acute effects, and will be labelled as such.

Diagnostics in the same fortnight: estimated squat 1RM relative to body mass, the one heuristic the collective rates high as a floor rule, with below 1.5 meaning strength-limited; drop-jump reactive strength index from five or more trials, moderate trust, best as a readiness monitor; body composition; hands-on-hips jump; countermovement depth and arm timing from video. The force-velocity profile is computed and filed as a tiebreaker only. The collective's trust in prescribing from it is low, since a randomized trial found no benefit from individualizing on it, and that trust weight is visible in the plan.

**Week 2: the variance question.** The agent asks the Commons what is heterogeneous in jump training for people like this. Answer, with current knowledge: the means of the big levers are well established and borrowed. Strength transfers below a relative squat of 1.5; plyometric progression adds 8 to 12% over ten weeks; technique is worth the first inch or two; each percent of fat mass lost is worth about 0.8 to 1% of height if force is retained. What varies between people enough to be worth personal identification: gross responsiveness to a strength block, the fatigue and fitness time constants, roughly 7 to 15 days and 30 to 50 days, tolerance of plyometric dose before reactive strength and tendon scores degrade, and adherence. The Self-Model gets four personal parameters. Everything else is prior.

**Week 2: the plan, the core and the budget.** The non-negotiable core is not an experimental variable, only its dose: two strength sessions and two plyometric or jump-skill exposures a week folded into three sessions; at least seven hours of sleep as a target the sleep quest owns; a body-composition target of minus 3 to 4 kg of fat over 16 weeks if body fat is above 15%. The prior assigns at least 80% of expected gain to this core. The experiment budget is capped at 10 to 15% of training time and attention. A four-weekly basics audit, covering estimated 1RM, contacts done, sleep, body mass and sessions completed, must pass before any new experiment launches. This is the guard against the structural failure every good coach predicts: acute experiments are statistically clean and chronic ones are messy, so an unguarded optimizer drifts toward caffeine trials while the squat stalls.

Period 1 is a 12-week strength-led block with low-intensity plyometric preparation: two to four weeks of landing and isometric work before any depth jump; contacts per session held at 80 to 100 and rising at most 10% a week; boxes under 45 cm; high-intensity stretch-shortening sessions at most twice a week and 48 to 72 hours apart; a deload every fourth week; creatine, which has strong population evidence, is cheap and reversible, and is borrowed without a personal test.

**Pre-registered forecasts, written before day 1 of the block.**

| Horizon | Forecast |
|---|---|
| 2 weeks | Test error 0.9 plus or minus 0.2 in. Jump down 5 plus or minus 2% the day after heavy squats, back to baseline by day 3. Technique work on depth and arm timing adds 0.5 to 1.0 in within 14 days. |
| 6 weeks | Estimated squat 1RM up 10 to 15%. Reactive strength index up 10 to 15%. Body mass down about 2 kg with the jump not lower. Jump up 0.5 to 1.5 in, 80% interval. Zero days of tendon pain at 4 or more. Adherence 85% or better. |
| 12 weeks | Mean of best three at 29.5 to 31.0 in, 80% interval. Approach up 2 to 3 in. Relative squat from about 1.3 to 1.8. No injury stoppage. A 10-day taper lifts the jump 2 to 3% over the block mean. |

**The experiments inside the block.** Two kinds, on two time scales, and the agent never confuses them.

Acute and reversible factors are identified by within-person randomization in days: warm-up A versus B, expected 3 to 5%; an external-focus cue versus none, 1 to 3%; caffeine at 3 to 6 mg per kg versus none, 2 to 4%; afternoon versus morning, 2 to 5%; post-activation potentiation after squats, 2 to 5% once the relative squat passes about 1.75, near zero or negative before. Each factor needs 6 to 10 randomized days at this noise level, assigned with logged probabilities, balanced over weekdays, with a washout of at least five half-lives for caffeine. The subject is told plainly what these buy: 3 to 6% on test day, stacked, and nothing on the ceiling. Their value is that the number the quest is scored on is a test-day number.

Chronic and cumulative adaptations are identified by designed block sequences rather than isolated comparisons. A constant program identifies nothing but its own steady state, so the agent varies load on purpose, with overload weeks, deloads and a terminal taper, and block lengths longer than the fast time constant. The taper response identifies the fatigue and fitness constants. The week at which reactive strength and the tendon score degrade identifies dose tolerance. Whether six weeks of strength plus a ten-day taper moved the jump by at least 2% identifies gross responsiveness. The agent states what this design cannot identify: the counterfactual best order of blocks, three-way interactions, the long-run ceiling, and whether another program would have done better. Those remain borrowed from the collective, and the plan says so.

**Weekly loop.** Measurements in; posteriors updated; the forecast band compared with the observation; leading indicators checked: morning tendon pain on a single-leg decline squat, pain lasting over 24 hours after a session, reactive strength down 10% on two sessions, jump down 5% for three days, resting heart rate up 5 to 7, two nights under six hours, body mass dropping faster than 2% a week. Micro-adaptation inside the envelope: a missed session is replanned the same day, a heavy day after a bad night is downgraded, a niggle converts the next plyometric exposure to isometrics. Hard stops are not negotiable. Tendon pain at 4 or more under load, or worse the next morning twice, means no plyometrics for seven days. Sharp pain, swelling, locking, giving way, night pain or bone-localized pain means stop impact and a physiotherapist within 72 hours. Any pain above 3 for more than 14 days means a physiotherapist. The agent cannot palpate or image and says so; the professional is a tool it prepares the case for, with the Ledger attached.

**When a forecast misses.** A miss is a branch, not a shrug. Below the 20th percentile of the forecast band the agent runs the diagnostic order the statistician pre-registered: measurement first, meaning the reach rule, frame rate, device, knee tuck on video, and a force-plate audit if available; then adherence from the exposure log; then acute fatigue, retesting 72 hours after a deload; then the model, asking whether the subject is a low responder to this stimulus, which is itself a parameter update that redirects period 2 toward reactive and technique work; then the ceiling. Each branch has its own test and its own forecast. Misses are confessed to the subject before they ask, and the updated model is shown.

**Cross-quest.** Sleep and vertical share the Self-Model. The sleep quest's extension to seven hours is forecast to be worth 2 to 5% on heavy days. The alcohol quest, if present, quotes the cost of a late drink in next-day jump and sleep latency, measured on this subject, and the subject decides.

**Court review before launch, one line each.** Domain critic: four weeks of extensive low-intensity contacts before any depth jump, not two. Statistician: the weekly test cannot detect anything in six weeks at this noise, so add a mid-week submaximal reactive-strength check as the early signal and widen the 6-week jump interval. Safety: no boxes above 60 cm until reactive strength exceeds 2.0 and the relative squat 1.5. Adherence: sessions capped at 60 minutes, isometric work moved into the warm-up so it is not skipped, a human accountability partner named. Evidence scout: nothing new that changes the priors this quarter; the force-velocity heuristic stays a tiebreaker. Pre-mortem: the first-block novelty gain will be mistaken for responsiveness, so the responsiveness parameter is scored on block two, not block one.

**Periods 2 to 6.** As the relative squat passes 1.5 to 1.8 the plan shifts weight toward reactive strength, depth jumps within the progression rules, and approach-jump skill, because that is where the collective says the next inches are for a strength-adequate jumper. Technique is front-loaded and retained; body composition is finished by week 16. The quest is re-chartered quarterly with the ladder's probabilities updated by the subject's own responsiveness and by the Commons. If this subject is a high responder, the 40-approach probability rises visibly. If not, the agent says what it sees as early as the data allow. A 3% quest resolving at 34 inches with a calibrated ledger is a success of the method, and the method is what the subject pays for.

**What the subject contributes.** Four parameters, the assignment probabilities, the exposure log and the scores, as sufficient statistics under privacy. Across fifty thousand such quests the Commons learns the distribution of strength-to-jump transfer by relative strength and age, the plyometric dose at which tendon scores degrade by phenotype, which cues work, which measurement protocols are least noisy, and it resolves under equipoise questions that sports science has argued for thirty years with twenty subjects at a time, such as whether individualizing on a force-velocity imbalance helps anyone, and whom.

**The expert's objections, and the loop's answers.**

| Objection | Answer |
|---|---|
| Noise of 4 to 5% against a true change of 1 to 2% a month; nothing can be attributed within a year | Correct, and the agent does not attribute. It forecasts, shrinks to the collective, and personalizes only four parameters. |
| Fitness-fatigue models are linear toys on a non-stationary subject | Simple robust models, wide priors, scored on predictive calibration, with an explicit admission of no counterfactual. |
| Reach, knee tuck, frame rate and device drift manufacture 2 to 4 inches | Pre-registered protocol, video on every trial, one device, periodic force-plate audit; "40" is defined as the mean of the best three under protocol. |
| Slow-onset tendinopathy from algorithmic progression, with no hands | Conservative caps, pain-gated progression, hard stops, referral rules, injury-risk forecasts in the Ledger, and the admission that no agent replaces a clinician's hands. |
| Accountability for a 3% outcome is theater, and a prior from self-selected self-reporters is garbage | The ladder with probabilities is scored, not the aspiration. The prior is seeded from the literature and weights user data by protocol compliance and video verification. |
| It will fiddle with caffeine while the squat stalls | The core's existence is not a variable, the experiment budget is capped, and the basics audit gates every new experiment. |

## 7. The same loop on the other quests

**Fixed exposure, minimize harm: the alcohol stays, the workload stays.** The quest estimates this person's dose-response to the exposure, by timing, food, pacing and hydration, on next-day objective measures and on sleep architecture with occasional gold-standard validation, by micro-randomization at the decision moment, and it states what cannot be mitigated. The agent never helps raise intake, and the stress quest must say when the workload is the disease.

**Decades and unobservable: colorectal cancer risk.** No within-person signal exists at any sample size and the agent says so. The honest objective is expected risk under a population causal model with measured intermediates. Personal experiments optimize only validated surrogates and screening adherence, forecasts are on those, and the Commons carries the long-run evidence. The agent interprets no test result itself; a clinician is the tool.

**Question-quests: does creatine help my dog, which one, how much.** The agent refuses "healthier" and substitutes measurables: body condition, collar activity, gait, stool score, cognitive tasks, vet labs. It may conclude that the value of information for this dog is near zero and that the population answer should simply be used, which no app says today. Longevity resolves only in the dog Commons, where a few thousand dogs under consented equipoise randomization produce in five years a trial nobody else will fund, with allometric dosing among the first conjectures tested.

**Capacity on a clock: fertility at 36.** The irreversibility of time shrinks the exploration budget to almost nothing. The plan is dominated by well-evidenced levers and timing, measurement is clinical, the clinician is in the loop from day one, and the agent's job is coordination, forecasting of markers, and adherence.

**Constraint quests: no knee pain while pursuing the goal, no back injury on the way to a 200 kg squat.** The constraint is the quest. The agent learns this person's load tolerance as a personal parameter, forecasts pain and load indicators weekly, and the envelope is the product.

**Two months, 3 to 5 kg.** Adherence-driven, with an eating-disorder screen at intake. The Self-Model's energy-balance state is shared with the vertical quest so the deficit never costs the jump.

## 8. Science as a byproduct

Randomized trials identify a mean effect. Within-person crossovers identify individual effects. A million scored, pre-registered, replicated within-person contrasts identify the distribution of effects and its predictors, including who it does not work for, which no trial can produce. The new objects are the Response Profile, a person's owned and portable set of causally identified response functions with uncertainty, an interventional phenotype; the Response Atlas, the population distribution of profiles by phenotype, what sequencing did for genotype; the Protocol Lemma, a validated reusable design such as "a 2 by 2 crossover with a five-day washout detects a 0.3-standard-deviation sleep effect in three weeks"; and the Ledger as a credential, which will eventually be demanded of human advice too. Surviving conjectures arrive at laboratories with pre-registered evidence, and responders who share a phenotype implicate a mechanism for the lab to confirm. "Know thyself" was never operationalized; the Response Profile is its operationalization. The framework does not replace trials for irreversible interventions. It dominates for reversible decisions of dose, timing, combination and behavior, which is most of the surface of a human life.

## 9. Objections that look strong, and what is actually unsolved

- **"You are experimenting on people."** With standing consent to randomization inside the set of options they already accept, with logged probabilities, with every question and result in a public registry. The undesigned life is already the experiment, only confounded. The limits are real: a right not to vary identity-level choices, no exploration of the irreversible, and exploration cost to the individual kept small and reversible.
- **"One subject has no power."** Within-person repeated measures, hierarchical shrinkage, decision rather than inference, and the variance question first. The honest floor remains: an effect of 0.2 standard deviations on a noisy daily proxy takes about two years of micro-randomization to resolve for one person, so such levers are borrowed or dropped.
- **"Expectancy is doing the work."** Blind where capsules allow, active comparators and objective endpoints elsewhere; otherwise the open-label effect including expectancy is accepted as this person's effect and never exported as mechanism.
- **"The ledger can be gamed by forecasting the trivial."** Proper scores, skill over persistence and population baselines, randomization for counterfactual checkability, holdout cohorts, immutable pre-registration.
- **"One learner means correlated error at scale."** Versioned priors validated prequentially on holdouts, concurrent time-stratified controls against drift, diverse agent stances, and the per-person variance test that lets your data overrule the prior.
- **"Language models hallucinate protocols."** They propose; the engine disposes; the library is curated with provenance; reality scores.
- **Unsolved, said plainly.** The signal-to-noise floor for small effects. The business model, since subscription churn reintroduces approval-seeking through the back door unless pricing is outcome-linked or payer-side. Measurement drift from device swaps. The liability precedent set by the first injury under a designed protocol.

## 10. Building it without dead ends

Invariants, true from the first commit:

1. Every action is a forecast; every forecast is scored against baselines by a proper rule; the Ledger is append-only and versioned.
2. Every assignment is logged with its probability and every exposure is time-stamped. Otherwise everything is observational and the collective dies.
3. The posterior lives in an explicit engine, never in prose. The language model proposes utility specs, protocols, explanations and conjectures; it never holds a belief or writes a score.
4. Every quest begins with the variance question, and "borrow, do not experiment" is a first-class answer.
5. Every measurement has a validity model, and the target outranks the proxy.
6. Exploration is bounded by worst-case posterior harm and indexed by reversibility; the irreversible is never explored on an individual.
7. The core of any plan is not an experimental variable, only its dose, and experiment budgets are capped.
8. Priors are versioned and validated on holdout cohorts; randomization has concurrent controls.
9. Raw data stays with the person; the Commons receives sufficient statistics under differential privacy, under a governance that forbids sale or transfer.
10. The harness is model-agnostic. The parts that improve with model capability, meaning design, critique, evidence synthesis and explanation, are delegated to models and swapped freely. The parts that must persist, meaning state, ledger, measurement and consent, are owned by the harness. Every model upgrade is scored on a replay of historical and synthetic users before it touches a person.

What not to build: a chatbot with plugins; protocol templates; a text memory of the person; a data lake before a design; a single agent; a vendor-locked model; a universal N-of-1 that runs before-after tests on cumulative or unobservable outcomes.

Order of work: the objects and the Ledger first. Then one fast-feedback quest end to end with the court, chosen among sleep timing levers, alcohol timing with intake fixed, and pain under a training goal, because these resolve nightly or daily with reversible levers. Then weight and the vertical jump. Then the Commons with privacy and consented equipoise. Then multi-quest coherence. Then the slow and clinical quests with clinicians in the loop.

Proof points that would convince the people who should build it: a thousand-user sleep quest with a calibration slope near one and a measurable advantage over an undesigned control in eight weeks; week-one forecasts for user ten thousand beating those for user one hundred, which is the collective prior made visible; six-month retention that survives the first confessed miss, with zero serious adverse events under the envelope; and, for the 3% quests, a success rate of about 3%, with non-responders called early.

The three arguments. The Ledger is the first credential in health that compounds, and no clinician, coach or chatbot can show one. Every subscriber is a participant, so the core asset is causal knowledge that gets cheaper per question as the population grows, the inverse of an engagement business. And the window is now: sensing is commodity, planning is good enough, and incumbents are structurally barred from randomizing and from publishing their misses. The models in the loop today are the worst that will ever be in it. The harness is what turns each better model into a better experimenter of you.
