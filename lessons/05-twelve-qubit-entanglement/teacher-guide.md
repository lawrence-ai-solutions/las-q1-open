# Twelve entangled qubits: all on or all off: teacher guide
**Level:** Advanced (ages 16+) · **Time:** about 45 minutes · From the LAS-Q1 open lesson pack (CC BY 4.0)

Link 12 qubits into one shared state, like a string of lights that is always all on or all off together, then prove the link is real.

## Learning goals
- Build a GHZ state with one H and a chain of CNOTs.
- Tell genuine entanglement from mere correlation using a parity measurement.
- Combine two measurements into a fidelity bound.

## Background for the teacher
H on one qubit followed by CNOTs along a chain makes the GHZ state (|000000000000> + |111111111111>)/sqrt(2): every measurement gives all 0s or all 1s. But a classical coin that sets all 12 bits the same would also do that. The difference shows up "sideways": applying H to every qubit before measuring, a true GHZ state always gives an even number of 1s (parity +1), while the classical mixture gives parity 0. The fidelity is at least (P_sync + parity)/2, and a value above 0.5 proves genuine 12-qubit entanglement.

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
| Fidelity bound (above 0.5 = entangled) | 1.00 | 0.68 | 0.646 | ibm_marrakesh | `dc31a72nj2vs73dhgo10` | data/18-twelve-qubit-ghz-christmas-lights |
| 12 ordinary coins all match | 0.05% |  | 0.08% | ibm_marrakesh | `dc31a72nj2vs73dhgo10` | data/18-twelve-qubit-ghz-christmas-lights |

Pre-registered; all three tests passed. All numbers come from the open dataset https://doi.org/10.5281/zenodo.24517586; see the Twin Check notebook to load and check them.

## Questions and answers
1. **For 12 ordinary coin flips, what is the chance that all 12 match?**
   *Answer:* 2 x (1/2)^12 = 1/2048, about 0.05%.
2. **Why is "always all on or all off" not enough to prove entanglement?**
   *Answer:* A classical device that picks all-0 or all-1 at random gives the same result; you need a second, sideways measurement.
3. **The real chip gave P_sync = 0.773 and parity = 0.519. Compute the fidelity bound. Is it entangled?**
   *Answer:* (0.773 + 0.519)/2 = 0.646, above 0.5, so yes: genuine 12-qubit entanglement (about 19 standard deviations above 0.5).
4. **All-on came up 34% and all-off 43%. Why might "off" be more common on real hardware?**
   *Answer:* Excited qubits decay back to 0 (T1 relaxation), so errors push outcomes toward 0.

---
Lawrence AI Solutions · Independent project, not affiliated with or endorsed by IBM. Real-hardware results are from IBM Quantum processors; model predictions are labelled as such.
