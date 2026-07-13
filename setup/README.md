# Setup: *Learn Quantum Computing with QiliSDK* (EuroPython 2026)

Please complete setup **before the session** and run `notebooks/00_setup.ipynb`. If its final cell shows a bar chart with two bars, `00` and `11`, each around 500 counts, you're ready.

You have two options: **local** or **Google Colab**. Either is fine; pick whichever you prefer.

---

## Option A: Local install (recommended if you have Python 3.11–3.13)

QiliSDK ships the **QiliSim** C++ simulator inside the wheel, so there is nothing to compile: `pip install qilisdk` just works on Windows, macOS, and Linux, and it pulls in everything the core tutorial needs (numpy, scipy, matplotlib) as dependencies.

### A1: with venv + pip

```bash
# 1. (recommended) create a fresh virtual environment
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# 2. install QiliSDK (+ a notebook UI if you don't have one)
pip install qilisdk jupyterlab

# 3. launch Jupyter and open notebooks/00_setup.ipynb
jupyter lab
```

### A2: with uv

If you use [uv](https://docs.astral.sh/uv/), it handles the Python version for you (it downloads a
supported interpreter if yours is too old or too new):

```bash
uv venv --python 3.13
source .venv/bin/activate        # Windows: .venv\Scripts\activate
uv pip install qilisdk jupyterlab
jupyter lab
```

**Requirements:** Python **3.11, 3.12, or 3.13**. Check with `python --version`.

> **Pin for an exact match (optional).** The tutorial is verified against `qilisdk 0.2.1`; use `pip install "qilisdk==0.2.1"` to match the notebooks exactly. (The Colab "Run me first" cells pin this version for you.)

---

## Extras: what the base install leaves out

`pip install qilisdk` runs **Parts 1–5** end to end. A few features ship as optional **extras** you
add in brackets, e.g. `pip install "qilisdk[openqasm,qir]"`:

| Extra | Adds | Used in |
|-------|------|---------|
| `openqasm` | OpenQASM 3 import / export | Part 6 interop demo |
| `qir` | QIR (LLVM-based) import / export | Part 6 interop demo |
| `qutip` | the `QutipBackend` (CPU simulation via QuTiP) | Part 6 (optional backend) |
| `cuda12` / `cuda13` | the `CudaBackend` (GPU simulation via NVIDIA CUDA-Q) | Part 6 (optional backend; needs an NVIDIA GPU) |
| `speqtrum` | the `SpeQtrum` client for Qilimanjaro's real QPUs | Part 6 (remote-hardware sketch) |
| `openfermion` | quantum-chemistry helpers | not used in this tutorial |

Part 6's optional-backend and interop cells are written to **degrade gracefully**: without the extra
they print a short "not installed" line telling you exactly which one to add, so nothing crashes.

**To run Part 6's interop demo** (OpenQASM / QIR export), add the two lightweight extras:

```bash
pip install "qilisdk[openqasm,qir]"
```

**For everything, including the GPU backend**, pick the one matching your CUDA toolkit:

```bash
pip install "qilisdk[all-cu12]"     # CUDA 12
pip install "qilisdk[all-cu13]"     # CUDA 13
```

`all-cu12` / `all-cu13` bundle *every* extra above (openqasm, qir, qutip, speqtrum, openfermion, and
the matching CUDA-Q backend). They are a large download, so they are only worth it if you want the GPU
backend; for the tutorial itself, `qilisdk` or `qilisdk[openqasm,qir]` is enough.

---

## Option B: Google Colab (zero local setup, needs internet)

Every tutorial notebook starts with a **"Run me first"** cell that installs QiliSDK automatically when
it is missing. On Colab you just:

1. Open the notebook in Colab (File → Upload notebook, or use the shared links we send).
2. Run the first cell (~1 min). Parts 1–5 install the base `qilisdk`; Part 6 additionally pulls the
   small `openqasm` + `qir` extras for its interop demo. (The GPU / QuTiP backends stay optional.)
3. Continue normally.

That same first cell is a **no-op locally** (if QiliSDK is already installed it does nothing), so the
notebooks are identical in both environments.

---

## Verify your environment

Run this anywhere (a cell, or `python -c`):

```python
import qilisdk
print(qilisdk.__version__)     # 0.2.1
print(qilisdk.about())         # full diagnostics: versions, system, QiliSim/QTensor import status
```

`notebooks/00_setup.ipynb` does this plus a 2-qubit Bell-circuit smoke test.

---

## Troubleshooting

| Symptom | Fix |
|---------|-----|
| `pip` can't find a matching `qilisdk` wheel | Check `python --version` is 3.11–3.13; upgrade pip: `pip install -U pip`. |
| Import works but `0.0.0` version | The dist isn't fully installed. Reinstall in a clean venv. |
| Plots don't show in Jupyter | Put `%matplotlib inline` at the top of the notebook (the tutorial notebooks already do). |
| Part 6 prints "extra not installed" | Expected on a base install. Add the extra it names, e.g. `pip install "qilisdk[openqasm,qir]"`. |
| Colab "restart session" prompt after install | Just re-run the cell; the install is cached for the session. |
| Anything else | Use Colab (Option B). It sidesteps all local-toolchain issues. |

Docs (EN / ES / CA): <https://qilimanjaro-tech.github.io/qilisdk/> · Source: <https://github.com/qilimanjaro-tech/qilisdk>
