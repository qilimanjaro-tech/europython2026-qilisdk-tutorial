# Presenter run-of-show

Narration script and screen-management plan for `qilisdk_tutorial.md`, paired with the
notebooks in `../notebooks/`. Designed for **a single projector screen**.

## The one-screen rule: "slides at the seams, notebook in the middle"

The deck is a **map, not a reference**. Its concept slides exist to *frame* each part
**before** you open its notebook, and to give clean **transitions** between parts.

- For each part: show its 2–3 concept slides (screen = **slides**), then **switch to the
  notebook and stay there** for the whole code-along + exercises, then return to slides
  **only** at the next divider.
- **Narrate concepts *before* the notebook, never after** — every notebook ends with its
  own recap cell, so a slides-after recap would just duplicate it.
- **Avoid back-and-forth.** On one screen each switch costs ~10–15 s plus a context break,
  and buys nothing: the notebook markdown re-teaches every concept exactly when the
  audience reaches it. The slides are the trailer; the notebook is the movie.
- **The one exception is the four image slides** (architecture, QTensor, noise, reservoir).
  They are not on the notebook screen, so they are your deliberate "flip-back" assets —
  especially the **architecture** slide at the Part 3 (digital→analog) and Part 6
  (execution) pivots, and the **reservoir** diagram when you reach notebook §6.4.

## Timing budget

Keep each part's slide framing to **2–4 min** so ~85% of every part is hands-on.

| Block | Screen | Budget |
|-------|--------|--------|
| Intro (title → notation) | slides | ~10 min |
| Part 1 slides → Notebook 01 | slides → notebook | ~3 + ~27 min |
| Part 2 slides → Notebook 02 | slides → notebook | ~3 + ~27 min |
| Part 3 slides → Notebook 03 | slides → notebook | ~4 + ~31 min |
| Break | slides (divider up) | 15 min |
| Part 4 slides → Notebook 04 | slides → notebook | ~4 + ~36 min |
| Part 5 slides → Notebook 05 | slides → notebook | ~3 + ~17 min |
| Part 6 slides → Notebook 06 | slides → notebook | ~4 + ~26 min |
| Close (journey, thanks) | slides | ~5 min + Q&A |

## Per-slide narration

Screen cue in **bold**; beats are talking points, not a word-for-word script.

### Intro — screen = SLIDES throughout (~10 min)

- **Title** *(SLIDES, 30 s):* hands-on tutorial — you'll *write* quantum programs today, not watch.
- **Me / Qilimanjaro / QiliSDK** *(1 min):* who you are; Qilimanjaro builds analog QPUs in Barcelona; QiliSDK is the open-source stack — **digital *and* analog** in one API, with a bundled C++ simulator.
- **Why quantum computing?** *(1.5 min):* three real motivations (quantum simulation and the 2ⁿ wall; optimization as energy minimization; ML feature maps) plus the day-one bonus of true randomness. These are the through-lines they'll *see* today.
- **Quantum in 2026** *(1.5 min):* expectation-setting — won't speed up Django; devices are small/noisy but real; the simulator is the smart entry; simulator code runs on hardware unchanged (Parts 5–6).
- **What you'll build** *(1 min):* name the six deliverables; stress "you write each one."
- **Links & QR codes** *(SLIDES, 30–45 s):* "Scan the left QR to get *this* tutorial repo and follow along; the other two are the QiliSDK source and the docs for later." Pause so people can scan before the `00_setup` step. *(This slide replaces the old Schedule slide, which is commented out in the `.md` — uncomment to restore it.)*
- **Follow along** *(SLIDES; briefly open `00_setup`, 2–3 min):* both run modes; "everyone run `00_setup` now — green if you see ~500/500 on `00`/`11`." Pause and walk the room until checks are green.
- **The architecture** *(SLIDES, `overall.jpg`, 1.5 min):* the day's mental model — Primitives → Functionals → Backends, one `execute()`. "We light up this map part by part." This is your flip-back asset.
- **How we'll work** *(1 min):* coding-first; concept → code-along → 1–2 exercises; attendee vs solutions notebooks; try before peeking.
- **30 seconds of notation** *(1 min):* ket = column vector; bra = its conjugate transpose; sandwich = one number (the average). → **switch to Notebook 01.**

### Part 1 — slides ~3 min, then Notebook 01 ~27 min

- **Divider** *(SLIDES, 20 s):* "Foundations — build the state itself, then measure it and average observables."
- **Part 1 ideas** *(SLIDES, 2 min):* qubit = 2 amplitudes; measuring = Born rule + collapse; n qubits = 2ⁿ amplitudes (memory wall, Feynman); you read only n bits out, so interference is engineered.
- **Part 1 vocab / API** *(SLIDES, 1.5 min):* prime the words (superposition, phase, observable/expectation, entanglement) and API (`QTensor`, `ket`, `.probabilities()`, `expect_val`, `partial_trace`). Don't explain deeply — the notebook does.
- **QTensor** *(SLIDES, `qtensor.jpg`, 30 s):* one object = states *and* operators; matrix ops + factories + QI primitives. → **Notebook 01** (§1.1–1.4, Ex 1.1 & 1.2). Teach *from the notebook prose.*

> Note: Part 1 is now **states-only** — no gates, no interference *demo*, no eavesdropper *demo*. Those are Part 2. Part 1 only establishes that `|+>` and `|->` are distinct states.

### Part 2 — slides ~3 min, then Notebook 02 ~27 min

- **Divider** *(SLIDES, 20 s):* "Now we *operate* on states — gates, circuits, execution."
- **Part 2 ideas** *(SLIDES, 2 min):* gates = reversible matrices (H→superposition, CNOT→entangle); circuit = ordered gates; measurement ends it; sampling vs exact. Add: "this is where interference becomes visible and where we catch an eavesdropper."
- **Part 2 execution pattern** *(SLIDES, 1.5 min):* dwell here — `execute(functional, readout)`, the call that recurs every part; the same call hits a real QPU in Part 6 by swapping one object. → **Notebook 02** (§2.1 gates + interference, §2.2 run/read, §2.2b BB84, §2.3 entanglement + Ex 2.1, §2.4 dice roller + Ex 2.2).

### Part 3 — slides ~4 min, then Notebook 03 ~31 min

- **Divider** *(SLIDES, 20 s):* "A different model — analog: one continuous physical process." *Flip `overall.jpg` back: "Digital → Analog primitives."*
- **Part 3 ideas** *(SLIDES, 2 min):* Hamiltonian = energy = cost over bitstrings; ground state = answer; annealing = start easy, morph slowly, stay in the minimum; "physics is the optimizer"; speed is a real knob (Ex 3.2).
- **Part 3 vocab / API** *(SLIDES, 2 min):* Paulis as building blocks; Ising = Z-terms = spins; adiabatic theorem (the guarantee); API `Hamiltonian` algebra, `Schedule.linear`, `AnalogEvolution`. → **Notebook 03.**

### Break — `Break` divider *(SLIDES)*, leave up for 15 min.

### Part 4 — slides ~4 min, then Notebook 04 ~36 min

- **Divider** *(SLIDES, 20 s).*
- **Variational loop** *(SLIDES, 2 min):* "it *is* an ML training loop" — ansatz = model, energy = loss, SciPy = optimizer; VQE minimizes measured energy; variational principle = approach from above; ran on hardware in 2016.
- **Python → physics** *(SLIDES, 2 min):* QUBO (+penalties); `Model → to_qubo() → to_hamiltonian()`; QAOA = trainable anneal; today's instance = 4 services / 2 servers. → **Notebook 04.**

### Part 5 — slides ~3 min, then Notebook 05 ~17 min

- **Divider** *(SLIDES, 20 s).*
- **Part 5 ideas** *(SLIDES, 2 min):* noise → mixtures → density matrix; channels with dev analogies (bit flip, amplitude damping/T₁, readout error); ideal→noisy = one argument; the real question = how much gate error can H₂ absorb.
- **Noise framework** *(SLIDES, `noise.png`, 30 s):* one `NoiseModel`, two engines (Lindblad analog / Kraus digital); "you don't need the math." → **Notebook 05.**

### Part 6 — slides ~4 min, then Notebook 06 ~26 min

- **Divider** *(SLIDES, 20 s).* *Flip `overall.jpg`: "Execution layer."*
- **Swapping backends** *(SLIDES, 2 min):* like swapping a DB driver / numpy→CuPy; same functional + readout on QiliSim/CUDA/QPU; OpenQASM = JSON for circuits, QIR = bytecode.
- **Transpilation** *(SLIDES, 2 min):* transpiler = compiler (instruction selection + register allocation); native gate set + limited connectivity; SABRE inserts SWAPs; multiplies gates → spends Part 5's budget.
- **Capstone QRC** *(SLIDES, `reservoirs.jpg`, 1.5 min):* fixed quantum system as feature extractor; only a linear numpy model trained; forecasts a noisy sensor. **This maps to notebook §6.4 — the one place worth flipping back to a slide mid-part** (show this diagram when you reach §6.4). → **Notebook 06.**

### Close — screen = SLIDES

- **The journey** *(1.5 min):* recap the arc (dice → schedule → molecule/placement → noise → compiled → forecast) and the one primitive set + one `execute()`.
- **Thank you:** docs / source / `about()` / SpeQtrum / "rerun bigger." Q&A.

---

*Regenerate the HTML after editing the deck:* `marp qilisdk_tutorial.md -o qilisdk_tutorial.html`
(or `npx @marp-team/marp-cli qilisdk_tutorial.md -o qilisdk_tutorial.html`). Do not hand-edit the HTML.
