# Bell test: beat the classical limit: student worksheet
Name: ______________________ Date: ____________

Make an entangled pair, measure it at tilted angles, and find agreement stronger than any non-quantum explanation allows.

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

## Questions
1. Run the circuit. What fraction of outcomes are 00 or 11?

   ______________________________________________________________

   ______________________________________________________________

2. Compute E = P(agree) - P(disagree) from your counts.

   ______________________________________________________________

   ______________________________________________________________

3. If all four settings gave |E| = 0.707 with the right signs, what is S?

   ______________________________________________________________

   ______________________________________________________________

4. Our real chip scored S = 2.74 +/- 0.02. Why does that matter?

   ______________________________________________________________

   ______________________________________________________________

---
LAS-Q1 open lesson pack · CC BY 4.0 · Lawrence AI Solutions
