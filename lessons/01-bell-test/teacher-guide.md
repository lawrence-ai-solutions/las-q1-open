# Bell test: beat the classical limit: teacher guide
**Level:** Intermediate (ages 15+) · **Time:** about 40 minutes · From the LAS-Q1 open lesson pack (CC BY 4.0)

Make an entangled pair, measure it at tilted angles, and find agreement stronger than any non-quantum explanation allows.

## Learning goals
- Measure an entangled pair at tilted angles.
- Compute a correlation E from counts.
- Explain why S > 2 rules out non-quantum (local) explanations.

## Background for the teacher
For a Bell pair measured at angles differing by theta, the two results agree with probability cos^2(theta/2). The CHSH score combines four settings: S = |E(a,b) + E(a,b') + E(a',b) - E(a',b')|. Any local hidden-variable theory gives S <= 2; quantum mechanics reaches 2*sqrt(2) = 2.83.

## Run it yourself (free tools)
- **Quirk** (drag-and-drop simulator in the browser): https://algassert.com/quirk
- **IBM Quantum Composer** (free account; can run on real hardware): https://quantum.cloud.ibm.com/composer
- **Qiskit** (Python, free; works in Google Colab):

```python
from qiskit import QuantumCircuit
import numpy as np
qc = QuantumCircuit(2, 2)
qc.h(0)               # qubit 0: equal superposition
qc.cx(0, 1)           # entangle: the pair is now 00 or 11
qc.ry(-np.pi / 4, 1)  # tilt the angle qubit 1 is measured at
qc.measure([0, 1], [0, 1])
```

OpenQASM version (paste into Composer):

```
OPENQASM 2.0;
include "qelib1.inc";
qreg q[2];
creg c[2];
h q[0];
cx q[0],q[1];
ry(-pi/4) q[1];
measure q -> c;
```

## What a real quantum computer measured
| Quantity | Perfect computer | Predicted before the run (LAS-Q1) | Real chip | Chip | Job ID | Dataset folder |
|---|---|---|---|---|---|---|
| Bell pair: the two qubits agree (00 or 11) | 100% | 98.9% | 99.0% | ibm_marrakesh | `dbufm7vf8rhs73bm62p0` | data/01-bell-and-teleport |
| CHSH score S (4 angle settings) | 2.83 | not predicted | 2.74 ± 0.02 | ibm_marrakesh | `dbufsdtarooc73fjrsog` | data/02-chsh-and-feedforward-teleport |

Any non-quantum (local hidden-variable) explanation scores at most S = 2. The real chip beat that by about 37 standard deviations. All numbers come from the open dataset https://doi.org/10.5281/zenodo.24517586; see the Twin Check notebook to load and check them.

## Questions and answers
1. **Run the circuit. What fraction of outcomes are 00 or 11?**
   *Answer:* About 85% ideally (cos^2 of 22.5 degrees = 0.854), a bit less on noisy devices.
2. **Compute E = P(agree) - P(disagree) from your counts.**
   *Answer:* Ideally 0.854 - 0.146 = 0.707.
3. **If all four settings gave |E| = 0.707 with the right signs, what is S?**
   *Answer:* S = 4 x 0.707 = 2.83.
4. **Our real chip scored S = 2.74 +/- 0.02. Why does that matter?**
   *Answer:* It is far above 2 (about 37 standard deviations), so no non-quantum model can explain the data.

---
Lawrence AI Solutions · Independent project, not affiliated with or endorsed by IBM. Real-hardware results are from IBM Quantum processors; model predictions are labelled as such.
