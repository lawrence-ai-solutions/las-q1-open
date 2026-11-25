# Twelve entangled qubits: all on or all off: student worksheet
Name: ______________________ Date: ____________

Link 12 qubits into one shared state, like a string of lights that is always all on or all off together, then test whether the link is genuine entanglement.

## Run it yourself (free tools)
- **Quirk** (drag-and-drop simulator in the browser): https://algassert.com/quirk
- **IBM Quantum Composer** (free account; can run on real hardware): https://quantum.cloud.ibm.com/composer
- **Qiskit** (Python, free; works in Google Colab):

```python
from qiskit import QuantumCircuit
N = 12
def ghz(sideways=False):
    qc = QuantumCircuit(N, N); c = N // 2
    qc.h(c)
    for k in range(1, N):                 # grow outward from the middle (shallower circuit)
        if c - k >= 0: qc.cx(c - k + 1, c - k)
        if c + k - 1 < N - 1: qc.cx(c + k - 1, c + k)
    if sideways: qc.h(range(N))           # read every light "sideways"
    qc.measure(range(N), range(N)); return qc
lights, twinkle = ghz(), ghz(sideways=True)
```

## What a real quantum computer measured
| Quantity | Perfect computer | Predicted before the run (LAS-Q1) | Real chip | Chip | Job ID | Dataset folder |
|---|---|---|---|---|---|---|
| All 12 in sync (all on or all off) | 100% | 75.1% | 77.3% | ibm_marrakesh | `dc31a72nj2vs73dhgo10` | data/18-twelve-qubit-ghz-christmas-lights |
| Sideways parity | 1.00 | 0.61 | 0.52 | ibm_marrakesh | `dc31a72nj2vs73dhgo10` | data/18-twelve-qubit-ghz-christmas-lights |
| Fidelity bound F >= P_sync + (parity - 1)/2 (above 0.5 = entangled) | 1.00 | 0.555 (post-run correction, from saved pre-run components) | 0.533 | ibm_marrakesh | `dc31a72nj2vs73dhgo10` | data/18-twelve-qubit-ghz-christmas-lights |
| 12 ordinary coins all match | 0.05% |  | 0.08% | ibm_marrakesh | `dc31a72nj2vs73dhgo10` | data/18-twelve-qubit-ghz-christmas-lights |

Pre-registered. Correction (25 Nov 2026): the originally registered fidelity formula, (P_sync + parity)/2, is not a valid bound; the values above use the correct bound recomputed from the same saved data (0.533, still above 0.5, about 3.5 standard deviations). All numbers come from the open dataset https://doi.org/10.5281/zenodo.24517586; see the Twin Check notebook to load and check them.

## Questions
1. For 12 ordinary coin flips, what is the chance that all 12 match?

   ______________________________________________________________

   ______________________________________________________________

2. Why is "always all on or all off" not enough to prove entanglement?

   ______________________________________________________________

   ______________________________________________________________

3. The real chip gave P_sync = 0.773 and parity = 0.519. Compute the fidelity bound F >= P_sync + (parity - 1)/2. Is it entangled?

   ______________________________________________________________

   ______________________________________________________________

4. All-on came up 34% and all-off 43%. Why might "off" be more common on real hardware?

   ______________________________________________________________

   ______________________________________________________________

---
LAS-Q1 open lesson pack · CC BY 4.0 · Lawrence AI Solutions
