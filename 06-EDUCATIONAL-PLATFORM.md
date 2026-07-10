# **The Educational Platform: Digital Coursework for the Training Port**
## Strategic White Paper on Teaching Robotics Assembly, AI-Assisted Design, and Programming Through SuperInstance's Own Paradigms

**Document Version:** 1.0
**Date:** July 10, 2026
**Status:** Proposal — grounded in the verified 2026 production-hardening round
**Depends on:** 04-TRAINING-PORT.md (the model this accelerates), 00-MANIFESTO.md, 01-FIELD-KIT-ARCHITECTURE.md, 05-COCAPN-FOUNDATION.md

---

## **Executive Summary**

The Training Port model (04-TRAINING-PORT.md) is deliberately physical: trust and skill propagate hand-to-hand, from Observer to Assistant to Technician to Trainer, on real boats with real consequences. That thesis is correct and this paper does not amend it. What the Training Port lacks is not a classroom — it is a **textbook**. There is currently no digital layer a trainee can study the night before their first shadow day, no reference an Independent Technician can pull up kneeling in a bilge, no structured path for a Trainer to hand a new cohort besides "come with me on the next install."

This paper proposes that digital layer, and it makes one claim that changes the economics of building it: **the curriculum's raw material already exists, and it has just been independently verified.** A production-hardening round across 25 SuperInstance repositories — executed by AI agents, with every claim re-verified by rebuild, retest, or fact-check before being trusted — has left behind real bytecode VMs, real protocol parsers, real buildable firmware, real hardware compatibility schemas, and, just as valuably, a documented record of real bugs found and fixed through human-AI collaboration. We do not need to invent example projects. The examples are sitting in git history.

The paper covers five things: how digital coursework plugs into each phase of the existing five-phase curriculum (an accelerant, never a substitute for supervised installs); a concrete curriculum outline across three tracks — **Robotics Assembly**, **AI-Assisted Design**, and **Programming** — built entirely from verified repos; the argument that SuperInstance's distinctive engineering culture (honesty markers, independent verification, git-as-memory) is itself the most defensible thing we can teach; genuine cross-repo synergies the coursework should exploit; and an honestly-scoped build plan whose first step is three markdown course outlines and one working exercise, not a platform.

Throughout, this paper practices the convention it argues for: ✅ marks what exists and was verified this round, ⚠️ marks what exists with known gaps, 🔮 marks proposals and aspirations. Nothing marked ✅ here is aspirational.

---

## **1. What the Port Cannot Teach Alone**

The Port-as-Academy argument in 04-TRAINING-PORT.md is that reality is the ultimate simulator: real problems on real assets, immediate high-stakes feedback, community oversight. A classroom cannot replicate a vibrating engine room, and we should not try.

But the apprenticeship model has three real constraints that a digital layer relieves without replacing anything:

1. **Trainer time is the scarcest resource in the network.** Every hour Casey spends explaining what a wire gauge is, or what a git commit is, is an hour not spent on the judgment-transfer that only he can do. The viral growth model's rate limit is trainer bandwidth. Digital coursework moves the *teachable-by-anyone* material off the dock so dock time is spent on the *teachable-only-by-a-master* material.

2. **The network has no shared floor.** Trainees arrive with wildly different baselines — one knows diesel hydraulics but has never opened a terminal; another writes Python but has never crimped a marine connector. Phase 1 (Observer) currently absorbs this variance on the trainer's time. A self-paced pre-Observer module gives every trainee the same vocabulary before their first shadow day.

3. **Knowledge decays between installs.** An Independent Technician doing three installs a month retains fluency. One doing three a season doesn't. The git-agent fleet preserves *what was done*; it does not currently teach *how to do it again*. Reference courses — short, searchable, pull-up-able mid-repair — are the missing complement to the fleet knowledge base.

The framing, then: **the Training Port is the academy; the Educational Platform is its library.** The library never graduates anyone. Phases 3 and 4 (supervised and independent installs) remain the only path to credentialing, exactly as designed. The platform accelerates entry into those phases and sustains competence after them.

---

## **2. The Raw Material Already Exists — and It Was Verified**

Most technical curricula are built on toy examples, and students can tell. What the 2026 production-hardening round left behind is different in kind: it is a body of **real, small, comprehensible systems** that a trainee can build, run, and audit — each one recently verified by an independent pass, not self-reported by the agent that wrote it.

The teaching-relevant inventory (each item ✅ verified this round unless marked otherwise):

- ✅ **nexus-edge-runtime** — ~2,973 lines across 10 modules: a 32-opcode bytecode VM deployable to ESP32/Jetson, a trust-scoring engine, a wire protocol, a 4-tier safety system, and an intent compiler (natural language → bytecode). Zero tests existed before this round; 85 were added, and in the process two real bugs were found: an assembler bug that packed negative float immediates incorrectly (a `struct.error`), and an off-by-2 payload-decode bug that silently dropped the first 2 bytes of every wire message.
- ✅ **fleet-midi** — a real MIDI-inspired event bus: `MidiMessage` enum, running-status parser, `FleetBroadcaster`, 12/12 tests, hand-verified against the actual MIDI 1.0 specification; since extended with a generalized Context frame (GPS + vessel ID) and binary codec with CRC8, 30/30 tests.
- ✅ **fleet-conductor** — an in-memory orchestration core (AgentState FSM, conservation guard, reconcile loop), 42/42 tests, clippy and fmt clean. Notably, this round *scoped it down* from an over-ambitious README to what could really be built — itself a lesson.
- ✅ **openconstruct-esp32** — real ESP32 sensor firmware whose `pio run -e esp32dev` build was verified to succeed after fixing a real `String::toLowerCase()` compile bug and adding the missing `platformio.ini`.
- ✅ **edge-equipment-catalog** — a JSON Schema plus five accurately-sourced hardware profiles (Raspberry Pi 4, Pi 5, Jetson Orin Nano, Jetson AGX Orin, BeagleBone Black — specs checked against public documentation, uncertain values flagged) and a working TypeScript compatibility checker. Built this round to replace a README that claimed "50+ hardware models" behind a 404 link.
- ✅ **edge-compiler** — a real Cloudflare Worker whose compile/quantize logic had never type-checked: 5 real TypeScript strict-mode errors found and fixed, one deploy-breaking (a function referenced `env` without receiving it). Its calls to `@cf/onnx` and `@cf/quantization` — model IDs that do not exist in Cloudflare's real Workers AI catalog — were marked honestly rather than faked.
- ✅ **kintsugi-math-c / spectral-mechanics / spectral-music-v2** — three tested C/math libraries, each of which contained a real correctness bug found by human+agent audit this round: `measure_resilience()` never read its own `CrackGraph` parameter (11/11 tests after the genuine rewrite); `virial_ratio` computed an instantaneous snapshot while its docstring implied a time-average, producing 385.86 where ~1.0 was claimed (9/9 tests after fixing); a greedy voice-assignment path could let multiple voices collide on one pitch (35/35 tests after fixing).
- ✅ **edge-relay-agent** — ~2,624 lines of real Python with 79/79 passing tests that had *no README at all*; one was written from source this round, honestly flagging three scope gaps (a `serve` command that is a heartbeat loop, not a real socket; a silently-unpersisted argument; a "discovery" that is a manual registry).
- ✅ **Edge-Native** — dissertation-scale documentation over a real ESP32 firmware VM and Jetson bytecode layer, independently verified excellent (3/3 C tests, 14/14 Python tests, real CI); this round's only fixes were two README claims.
- ✅ **The honesty-audit corpus** — vessel-room-navigator (gauges and "AI chat" that were `Math.random()` jitter and a keyword parser, presented as live; plus a demo that never actually loaded because `init()` threw on a nonexistent element), vessel-bridge ("the bridge doesn't bridge" — hardware paths stubbed while presented as functional; 14 real tests added including one that explicitly documents the testability gap), gravity-well-protocol (a README-only repo written as if deployed software existed, down to a fictional 32KB JS file), open-mythos-edge (a genuinely substantial PyTorch transformer, on PyPI — whose CI was fake-green via `pytest ... || true` over zero test files).

This inventory matters strategically because it converts curriculum development from a *content-creation* problem into a *content-curation* problem. The exercises exist; the bugs-as-lessons exist in git history with their fixes; the verification record exists. What's missing is the pedagogical scaffolding around them.

---

## **3. Integration with the Five Phases: Where Digital Coursework Plugs In**

The five-phase curriculum from 04-TRAINING-PORT.md stays exactly as written. Digital coursework attaches to it as follows:

| Phase | Physical (unchanged) | Digital layer (new) |
|-------|---------------------|---------------------|
| **Phase 0 — Pre-Observer** | *(does not exist today)* | Self-paced foundation module, ~4–6 hours: what the Field Kit is, what a git repo is, the Photo Protocol from 02-VIBE-CODING-PHYSICAL.md, safety vocabulary, and the honesty-marker convention. Goal: every Observer arrives speaking the same language. |
| **Phase 1 — Observer (1 day)** | Shadow a full install | Evening companion module: annotated walkthrough of a real installation repo — the actual commits, photos, and decision log from an install like the one they just watched. Reinforces "the repo is the manual" while the memory is fresh. |
| **Phase 2 — Assistant (1–2 days)** | Hands-on assist | The first Track exercises (Section 4): build the openconstruct-esp32 firmware, run the edge-equipment-catalog compatibility checker against the kit they just handled. Done at home, reviewed by the trainer in minutes, not hours. |
| **Phase 3 — Technician (supervised, 3–5 installs)** | Lead with oversight | The verification katas (Section 5): trainee audits a deliberately re-broken branch of a real repo and must find the real, historical bug. Trainer signs off on the kata alongside the install. |
| **Phase 4 — Independent Technician** | Solo installs | **Reference mode**, not course mode: searchable, offline-capable quick-reference versions of every module, designed to be pulled up mid-repair on the phone or the Field Kit's local web UI (01-FIELD-KIT-ARCHITECTURE.md already serves a Starlette app at `jetson.local:8080` — the reference library belongs there, on-device, air-gap-safe). |
| **Phase 5 — Trainer** | Train others, contribute patterns | Course-contribution track: Trainers convert their own field patterns into new modules and katas, exactly as they already contribute installation patterns to the fleet knowledge base. The curriculum becomes another git-native, fork-first artifact under Cocapn's model (05-COCAPN-FOUNDATION.md). |

Two design rules fall out of this table:

1. **No module ever gates a phase transition on its own.** Digital completion is evidence a trainer considers, never a credential. The credential remains the supervised install. This keeps the trust economics of 04-TRAINING-PORT.md intact — a certificate you can earn alone in a bedroom is exactly the Silicon Valley failure mode the model exists to avoid.
2. **Everything must work air-gapped.** Per the Manifesto, "on a 120-foot longliner in the Bering Sea in January, the cloud is a fantasy." Course content is markdown in git repos, synced to the Field Kit like any other agent repo, and readable at `jetson.local`. A trainee in Dutch Harbor with no signal has the full library. 🔮 A hosted web version is a convenience layer on top, never the source of truth.

---

## **4. The Three Tracks: A Real Curriculum Outline**

Each track is a sequence of modules; each module names its real source repo, what the trainee does, and which phase it serves. Course *outlines* follow — producing the full materials is Section 7's job.

### **Track A: Robotics Assembly** (serves Phases 0–2, reference mode in Phase 4)

*The claim: you cannot install what you do not understand physically. This track takes a trainee from "what is a single-board computer" to "I built and flashed a sensor node."*

- **A1 — Hardware Fundamentals** *(source: edge-equipment-catalog ✅)*. The five verified hardware profiles (Pi 4, Pi 5, Jetson Orin Nano, Jetson AGX Orin, BeagleBone Black) are the reading material — real specs, sourced from public documentation, with uncertain values honestly flagged in the data itself. Exercise: run the TypeScript compatibility checker against a proposed workload and explain, in writing, why the board it rejects gets rejected. This is precisely the reasoning a technician does when a captain asks "can this box run cameras too?"
- **A2 — The Field Kit, End to End** *(source: 01-FIELD-KIT-ARCHITECTURE.md ✅ as spec)*. Walk the Jetson Field Kit spec: the Pelican enclosure, the 12V/PoE power paths, the SD-to-NVMe provisioning boot sequence, the three-tier connectivity ladder. Exercise: trace the boot sequence scripts and answer failure-mode questions ("the kit boots from SD but never clones — what file do you check?").
- **A3 — First Physical Build** *(source: openconstruct-esp32 ✅)*. Clone the repo, run `pio run -e esp32dev`, flash a real ESP32, wire a real sensor. This build is verified to succeed as of this round — a trainee who fails is debugging their environment, not our content, and *that debugging is itself the lesson*. This is the track's capstone before Phase 2 dock work.
- **A4 (reference) — Protocol Bridges and Constrained Targets** *(sources: marine-gpu-edge ✅ protocol-bridge code with 13 real tests; Edge-Native ✅ firmware VM)*. Not a beginner module: reference material for Phase 4 technicians on how data moves between a microcontroller and a Jetson-class brain.

### **Track B: AI-Assisted Design** (serves Phases 2–3, and it is the culture carrier)

*The claim: the technician of the Paradigm works **with** an AI, and the round just completed is the most honest dataset anywhere on what that collaboration actually looks like — including where the AI is wrong.*

This track's spine is the **vibe-coding loop from 02-VIBE-CODING-PHYSICAL.md**, taught not through hypotheticals but through this round's real transcripts-in-git:

- **B1 — The Collaboration Loop**. The eight-stage VCPS workflow (discovery, understanding, design, vibing, implementation, validation, testing, documentation), using a real installation repo as the worked example.
- **B2 — When the AI Is Wrong: Reading the Round-3 Record** *(sources: all ✅)*. Case-study module built from real events: aider *hallucinating tests it never wrote* in persona-engine (the fix: 21 real tests written directly, including a schema-drift check against the 4 real committed character fixtures); a stray 0-byte file in holodeck-c named after an entire agent prompt — fossil evidence of an agent misreading its own instructions; edge-compiler's follow-up agent introducing its own mistake, caught in review. The lesson is the Manifesto's line made operational: *the AI handles complexity, the technician handles judgment* — and judgment includes judging the AI.
- **B3 — Auditing AI Output: The Math Libraries** *(sources: kintsugi-math-c ✅, spectral-mechanics ✅, spectral-music-v2 ✅)*. Three real audits, each with a one-sentence smell a non-mathematician can learn: a function that never reads its own parameter (`-Wextra` finds it); a result of 385.86 where the documentation promises ~1.0 (run the code and *look at the number*); a tracking array that is written but never read. Exercise: given each pre-fix commit, find the bug before reading the fix.
- **B4 — Production Hardening as a Discipline** *(source: edge-compiler ✅)*. Walk the five real strict-mode TypeScript errors, including the deploy-breaking un-passed `env`, and the honest marking of `@cf/onnx` / `@cf/quantization` as nonexistent model IDs rather than pretending they resolve. Companion example: nexus-git-agent's `master` branch that could not build at all until a mangled CSP header was fixed — "committed" and "working" are different claims, and only a build proves the second.

### **Track C: Programming** (serves Phases 2–4)

*The claim: a technician-programmer's path should run from bytes to systems on real SuperInstance infrastructure, so that by the end they can read the actual code running on their own Field Kit.*

- **C1 — Bytes on a Wire** *(source: fleet-midi ✅)*. The ideal first protocol: small enough to hold in your head, real enough to matter. Trainees walk the running-status parser byte by byte against the MIDI 1.0 spec — as this round's engineer literally did by hand — then extend to the Context frame (timestamp + GPS + vessel ID) and CRC8 codec. 30/30 tests exist as the safety net; the exercise is to break one and understand why it fails.
- **C2 — A Real VM, Small Enough to Learn** *(source: nexus-edge-runtime ✅)*. The 32-opcode bytecode VM is a genuinely rare teaching asset: a complete, deployable execution engine under 3,000 lines total across the runtime. Modules: the VM itself, then the wire protocol (see C3), then the 4-tier safety system, then the intent compiler (NL → bytecode) as the bridge back to Track B.
- **C3 — The Verification Capstone: Two Real Bugs** *(source: nexus-edge-runtime ✅)*. The two bugs found this round are a ready-made final exam. The off-by-2 payload decode — silently dropping the first 2 bytes of every message — is the perfect protocol bug: everything "works," and everything is wrong. The negative-float-immediate assembler bug teaches binary encoding pitfalls. Exercise format: the pre-fix commit is checked out; the trainee has the 85-test suite minus the specific regression tests; find the bugs, write the failing tests, then compare against the real historical fix.
- **C4 — Orchestration and State** *(sources: fleet-conductor ✅, edge-relay-agent ⚠️)*. The AgentState FSM, conservation guard, and reconcile loop (42/42 tests) as the intro to fleet coordination — conceptually the trainee's first step toward understanding Cocapn's `fleet-orchestrator` (05-COCAPN-FOUNDATION.md). edge-relay-agent is deliberately included *with its honestly-documented gaps* (heartbeat-not-socket `serve`, unpersisted `url`, manual "discovery"): reading a README that tells the truth about scope is a skill, and writing one is the exercise.

---

## **5. Teaching the Culture: Verification as Craft**

The most strategically important thing this round produced is not code. It is a **demonstrated engineering culture**, visible and consistent across 25 repos, that almost no one else teaches:

1. **Honesty markers as first-class syntax.** ✅ verified / ⚠️ real-with-gaps / 🔮 aspirational, applied to one's *own* claims. gravity-well-protocol's rewrite is the canonical example: the fake "Live Demo" link and fictional 32KB JS file were removed, but the real design ideas (region-limited broadcasts, traffic-informed gossip) were *kept* — as clearly-marked concepts. Honesty is not deletion; it is accurate labeling.
2. **Independent verification before trust.** Every finding in this round was re-verified — rebuilt, retested, or fact-checked — before being believed, including (especially) the agents' own self-reports. persona-engine is the object lesson: the agent *said* it wrote tests; it had not.
3. **Git as memory.** Already the Paradigm's foundation (00-MANIFESTO.md, 05-COCAPN-FOUNDATION.md); the educational insight is that git history is also the *curriculum's* substrate — every kata in this paper is "check out the pre-fix commit."
4. **Never present simulated as real.** vessel-room-navigator's `Math.random()` gauges and vessel-bridge's stubbed hardware paths were this round's cautionary tales; edge-native-paper's unsupported "10 vessels, 99.9% uptime" claim was reframed as a planned validation rather than asserted or deleted, because no in-repo telemetry could verify it either way. Even self-flattering numbers get corrected in *both* directions: superinstance-architecture understated the ecosystem (claimed 2,000–3,200 repos; real count 4,095; claimed 145,000+ lines of Rust; real count 373,639) and overstated a fork's freshness (claimed "1 ahead, 7 behind"; real: 4 ahead, 2,132 behind).

Why teach this explicitly rather than let it rub off? Because it is the differentiator that survives commoditization. Every trade school will eventually teach "prompt an AI to write firmware." Almost none will teach *how to catch the AI lying*, or how to write ⚠️ next to your own work. In a network whose entire business model is trust propagation (04-TRAINING-PORT.md's flywheel: trust is the currency), a workforce trained to verify-before-trust and label-before-shipping is the moat. A captain who has watched his technician say "this reading is simulated until I hook the real sensor — here's the marker that says so" trusts that technician more, not less.

**Pedagogical form — the Verification Kata.** Every module in every track ends with one: a real, historical bug or overclaim, re-broken on a branch, that the trainee must find, demonstrate with a failing test (or a failing *fact-check*, for documentation katas like codespace-edge-rd's wrong VM-RAM spec or Edge-Native's "21 specs" that were really 10), and fix. The round just completed generated at least a dozen of these across difficulty levels, from "run the build" (nexus-git-agent) to "audit the physics" (spectral-mechanics). 🔮 Over time, Phase 5 Trainers contribute new katas from field incidents, making the kata library a living artifact like the fleet knowledge base.

---

## **6. Cross-Repo Synergy: Connections the Curriculum Should Exploit**

The user's directive for this round was to "polish all of these and synergize their abilities." Three synergies are justified by what was actually read and verified — plus one flagged consolidation question:

1. **fleet-midi → nexus-edge-runtime wire protocol (the protocol ladder).** These are the same subject at two difficulty levels: both are compact binary framing protocols with real parsers and real test suites. fleet-midi is small (a hand-verifiable spec, running-status compression, CRC8) and nexus-edge-runtime's wire protocol is the production step up — and its historical off-by-2 payload bug is the *exact* class of error the fleet-midi module trains you to see. Track C sequences them deliberately (C1 → C3). Beyond curriculum: 🔮 as the fleet-midi event bus grows into the fleet-wide multi-sensor bus (Phase 2: persistence layer, currently designed but not started), the two protocols should share framing conventions rather than diverge — the curriculum pairing will make any divergence embarrassing, which is the point.

2. **edge-equipment-catalog → Field Kit onboarding and the Cocapn Equipment Protocol.** 01-FIELD-KIT-ARCHITECTURE.md specifies exact hardware; 05-COCAPN-FOUNDATION.md defines an "Equipment Protocol" where sensors and compute are abstracted behind a standardized schema — but that protocol has had no concrete public schema implementation. edge-equipment-catalog's JSON Schema + verified profiles + working TypeScript compatibility checker is, today, the closest real artifact to that protocol's hardware half. 🔮 Recommendation: adopt the catalog's schema as the Equipment Protocol's hardware-profile format, and put the compatibility checker into the Field Kit provisioning flow ("will this captain's requested workload fit this kit?") — turning a teaching aid into an operational tool, and vice versa.

3. **The honesty-audit corpus → the trust-scoring engine.** nexus-edge-runtime contains a trust-scoring engine; 04-TRAINING-PORT.md says trust "measured through reputation scores" is the network's currency. The verification katas produce, as a natural byproduct, exactly the kind of evidence a reputation system needs: verifiable, git-committed demonstrations that a specific technician found a specific real bug. 🔮 Long-term, kata completions signed into a trainee's own repo history could feed the same trust-scoring machinery — credential-by-commit-history rather than credential-by-certificate. This is marked 🔮 deliberately: it requires design work on gaming-resistance and should not gate anything until a Trainer countersignature model exists.

4. ⚠️ **Consolidation flag: two bytecode VMs.** Edge-Native contains a real, well-tested ESP32 firmware VM with a Jetson bytecode layer; nexus-edge-runtime contains a real 32-opcode VM targeting the same two platforms. Both are genuine and verified. Whether they should converge is an engineering decision beyond this paper's scope — but the curriculum must pick **one** as its teaching VM (this paper picks nexus-edge-runtime for its size and its usable bug history), and the existence of two is a signal the platform roadmap should resolve rather than paper over.

---

## **7. What to Build Next — Honestly Scoped**

The temptation is a platform: accounts, progress tracking, video, badges. The Training Port's own history argues the opposite — start with one technician, one port, one repo. The equivalent here:

**Step 1 (build now — small, real, immediately usable):**
A single new repository, `the-technician-courses`, containing:
- The three track outlines from Section 4 as structured markdown — one file per module, each linking to its real source repo and stating which phase it serves.
- **One fully-worked exercise**, end to end: Module A3 (the openconstruct-esp32 build), because its build success is already verified (`pio run -e esp32dev`), its parts cost is trivial, and it produces a physical object a trainee can hold. Include the full expected transcript: clone, build, flash, sensor reading, and the three most likely failure modes with fixes.
- **One verification kata**, packaged: the fleet-midi byte-walk (C1) — the pre-change parser on a branch, the MIDI 1.0 references, and the "break one test and explain why" exercise. Chosen because it needs no hardware at all, so it works for a Phase 0 trainee anywhere.
- A `CULTURE.md` teaching the honesty-marker convention, with the gravity-well-protocol rewrite as its worked example.

This is a few days of curation, not months of production. It is usable by the first real trainee the week it lands.

**Step 2 (after the first trainee uses Step 1):**
- Package 3–5 more katas directly from round-3 history (the C3 nexus bugs, the B3 math audits, the nexus-git-agent build-failure drill). The bugs and fixes are already in git; packaging is branch-creation plus a README each.
- Sync the course repo onto the Field Kit image so the library is served air-gapped at `jetson.local` alongside the existing Starlette UI (01-FIELD-KIT-ARCHITECTURE.md) — courses become just another git-synced repo under `/opt/captain/repos/`, which is architecturally free.

**Step 3 (🔮 — only if Steps 1–2 show real trainee pull):**
- 🔮 A static site (the reading layer only — content stays in git; the site is a render).
- 🔮 Kata-completion records feeding the trust-scoring integration from Section 6.3, gated on Trainer countersignature design.
- 🔮 Video walkthroughs of the physical modules, shot on real installs per the Photo Protocol.
- 🔮 An LMS-lite Worker for cohort tracking — explicitly last, and possibly never: if git history plus Trainer judgment tracks progress adequately (and in this culture it should), an LMS is overhead, not infrastructure.

What we are deliberately **not** building: accounts before there are users, certificates before there are Trainers to countersign them, and any content whose underlying claim we have not verified ourselves. deckboss-1 stays out of the curriculum entirely — it is archived, and teaching from deprecated material is a small dishonesty of its own.

---

## **8. Success Metrics**

Extending 04-TRAINING-PORT.md's network-vitality metrics rather than inventing parallel ones:

- **Trainer-hours saved per cohort:** the platform's entire justification. Measured by asking Trainers, not by dashboard telemetry we don't have. (This paper models its own rule: no invented baseline numbers. The current figure is unknown; establishing it is part of Step 1's first use.)
- **Time from Observer to Independent** (already a 04 metric): does the digital layer shorten it?
- **Kata completion → field-error correlation** 🔮: eventually, do technicians who complete verification katas produce fewer callback-generating installs? Trackable only once both sides have real volume.
- **Curriculum commits from Phase 5 Trainers:** the platform is healthy when the people it trained are writing it — the same viral loop as the Training Port itself.

---

## **9. Conclusion: The Library Next to the Dock**

The Technician Paradigm's founding claim is that the physical world's intelligence will be built by trusted humans augmented by AI, and that this trust propagates person to person, install to install. Nothing in this paper dilutes that. What this paper adds is the observation that SuperInstance has — partly by design, partly as a byproduct of doing a genuinely honest production-hardening round — accumulated the raw material for a technical education no one else can offer: real systems small enough to learn, real bugs preserved with their fixes, and a working demonstration of the verification culture that catches them.

The port teaches judgment. The library teaches everything judgment shouldn't be wasted on. Build the library one shelf at a time, starting with one repo, three outlines, one buildable exercise, and one kata — and let the same people the port trains fill the rest of the shelves.

---

**Appendix A: Honesty-Marker Legend (as used throughout this document)**
- ✅ Exists and was independently verified in the 2026 production-hardening round (rebuilt, retested, or fact-checked).
- ⚠️ Exists, is real, but has known and documented gaps.
- 🔮 Proposal or aspiration. Does not exist. Do not cite it as if it does.

**Appendix B: Source Repositories by Module**

| Module | Repo | Verified state |
|--------|------|----------------|
| A1 | edge-equipment-catalog | ✅ schema + 5 sourced profiles + working TS checker |
| A3 | openconstruct-esp32 | ✅ `pio run -e esp32dev` build success |
| A4 | marine-gpu-edge, Edge-Native | ✅ 13 protocol-bridge tests; ✅ 3/3 C + 14/14 Python tests |
| B2 | persona-engine, holodeck-c, edge-compiler | ✅ 21 real tests; ✅ 50 tests running (was 14); ✅ 5 strict-mode fixes |
| B3 | kintsugi-math-c, spectral-mechanics, spectral-music-v2 | ✅ 11/11, 9/9, 35/35 tests |
| B4 | edge-compiler, nexus-git-agent | ✅ deploy-breaking bugs fixed in both |
| C1 | fleet-midi | ✅ 12/12 core, 30/30 with event-bus extension |
| C2–C3 | nexus-edge-runtime | ✅ 85 tests added, 2 real bugs found and fixed |
| C4 | fleet-conductor, edge-relay-agent | ✅ 42/42 tests; ⚠️ 79/79 tests, 3 documented scope gaps |
| Culture | gravity-well-protocol, vessel-room-navigator, vessel-bridge, open-mythos-edge, edge-native-paper, superinstance-architecture | ✅ honesty rewrites and fact-checks, all verified |
