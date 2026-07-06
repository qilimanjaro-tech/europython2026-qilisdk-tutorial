# Learn Quantum Computing with QiliSDK

Material for the EuroPython 2026 hands-on tutorial *Learn Quantum Computing with QiliSDK: From
Circuits to Pulse-Level Control* (~3 hours, no quantum background required, Python 3.11–3.13).

## Where everything is

| Path | What it is |
|------|------------|
| [`setup/README.md`](setup/README.md) | Install instructions (pip, uv, or Google Colab). Start here. |
| [`notebooks/`](notebooks/) | The six tutorial notebooks (`00_setup` to `06_execution_and_hardware`), attendee versions with blank exercises. |
| [`notebooks/solutions/`](notebooks/solutions/) | The same notebooks with exercises solved and outputs included. |
| [`slides/`](slides/) | The Marp slide deck (`qilisdk_tutorial.md`, pre-rendered `qilisdk_tutorial.html`). |

## Quick start

```bash
pip install -r setup/requirements.txt
jupyter lab notebooks/00_setup.ipynb
```

If the last cell shows a bar chart with two bars, `00` and `11`, each around 500 counts, you are
ready for the session.
