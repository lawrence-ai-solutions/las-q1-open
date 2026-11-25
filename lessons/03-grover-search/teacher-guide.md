# Grover search: find 010 among 8: teacher guide
**Level:** Intermediate (ages 15+) · **Time:** about 35 minutes · From the LAS-Q1 open lesson pack (CC BY 4.0)

Search 8 possibilities for the marked one. Classical guessing needs about 4 tries on average; Grover needs 2 rounds.

## Learning goals
- Describe the oracle and diffuser steps.
- Compare Grover's 2 rounds with classical guessing.
- See how noise limits deep circuits.

## Background for the teacher
Grover's algorithm finds a marked item among N in about sqrt(N) rounds. For N = 8, two rounds give 94.5% success. The oracle flips the sign of the marked state; the diffuser reflects all amplitudes about their average, growing the marked one.

## Run it yourself (free tools)
- **Quirk** (drag-and-drop simulator in the browser): https://algassert.com/quirk
- **IBM Quantum Composer** (free account; can run on real hardware): https://quantum.cloud.ibm.com/composer
- **Qiskit** (Python, free; works in Google Colab):

```python
from qiskit import QuantumCircuit
def grover_round(qc):
    qc.x([0, 2]); qc.h(2); qc.ccx(0, 1, 2); qc.h(2); qc.x([0, 2])   # oracle: flip the sign of 010
    qc.h([0, 1, 2]); qc.x([0, 1, 2])                                 # diffuser
    qc.h(2); qc.ccx(0, 1, 2); qc.h(2)
    qc.x([0, 1, 2]); qc.h([0, 1, 2])
qc = QuantumCircuit(3, 3)
qc.h([0, 1, 2])
grover_round(qc); grover_round(qc)
qc.measure([0, 1, 2], [0, 1, 2])
```

## What a real quantum computer measured
| Quantity | Perfect computer | Predicted before the run (LAS-Q1) | Real chip | Chip | Job ID | Dataset folder |
|---|---|---|---|---|---|---|
| 1 round: found 010 | 78.1% | 70.3% | 70.4% | ibm_fez | `dbup9nn82tmc73dtqni0` | data/08-grover-search |
| 2 rounds: found 010 | 94.5% | 77.4% | 78.7% | ibm_fez | `dbup9nn82tmc73dtqni0` | data/08-grover-search |
| random guessing | 12.5% |  |  |  |  |  |

Predictions were saved before the run. Deeper circuits collect more error, which is why 2 rounds fall short of 94.5%. All numbers come from the open dataset https://doi.org/10.5281/zenodo.24517586; see the Twin Check notebook to load and check them.

## Questions and answers
1. **What is the chance of guessing the answer in one random try?**
   *Answer:* 1/8 = 12.5%.
2. **Run with 1 round (delete the second oracle + diffuser). What is the success rate?**
   *Answer:* About 78% ideally.
3. **Why does a third round make things worse?**
   *Answer:* Grover overshoots: amplitude rotates past the marked state, so success falls (to about 33%).
4. **The real chip found 010 78.7% of the time with 2 rounds. Why lower than 94.5%?**
   *Answer:* Gate errors, decay and readout errors on real hardware; deeper circuits accumulate more error.

---
Lawrence AI Solutions · Independent project, not affiliated with or endorsed by IBM. Real-hardware results are from IBM Quantum processors; model predictions are labelled as such.
