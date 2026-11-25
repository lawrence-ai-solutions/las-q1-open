# Teleportation with live feed-forward: teacher guide
**Level:** Intermediate (ages 15+) · **Time:** about 40 minutes · From the LAS-Q1 open lesson pack (CC BY 4.0)

Move a qubit's state to another qubit using one entangled pair, two measurements and corrections applied mid-circuit.

## Learning goals
- Follow the teleportation protocol step by step.
- Explain mid-circuit measurement and feed-forward.
- Check that the state arrived.

## Background for the teacher
Alice holds a message qubit and half of a Bell pair; Bob holds the other half. Alice measures her two qubits; her two classical bits tell Bob which correction (X and/or Z) recovers the message. No information travels faster than light: Bob needs Alice's bits.

## Run it yourself (free tools)
- **Quirk** (drag-and-drop simulator in the browser): https://algassert.com/quirk
- **IBM Quantum Composer** (free account; can run on real hardware): https://quantum.cloud.ibm.com/composer
- **Qiskit** (Python, free; works in Google Colab):

```python
from qiskit import QuantumCircuit
import numpy as np
qc = QuantumCircuit(3, 3)
qc.ry(np.pi / 3, 0)          # the message: reads 1 about 25% of the time
qc.h(1); qc.cx(1, 2)         # Alice (qubit 1) and Bob (qubit 2) share a Bell pair
qc.cx(0, 1); qc.h(0)         # Alice combines the message with her half
qc.measure(0, 0); qc.measure(1, 1)
with qc.if_test((qc.clbits[1], 1)): qc.x(2)   # Bob's corrections, decided mid-circuit
with qc.if_test((qc.clbits[0], 1)): qc.z(2)
qc.measure(2, 2)
```

OpenQASM version (paste into Composer):

```
OPENQASM 3.0;
include "stdgates.inc";
qubit[3] q;
bit[3] c;
ry(pi/3) q[0];
h q[1];
cx q[1], q[2];
cx q[0], q[1];
h q[0];
c[0] = measure q[0];
c[1] = measure q[1];
if (c[1] == 1) { x q[2]; }
if (c[0] == 1) { z q[2]; }
c[2] = measure q[2];
```

## What a real quantum computer measured
| Quantity | Perfect computer | Predicted before the run (LAS-Q1) | Real chip | Chip | Job ID | Dataset folder |
|---|---|---|---|---|---|---|
| Message arrives: Bob reads 1 | 25.0% | 25.6% | 28.4% | ibm_marrakesh | `dbufm7vf8rhs73bm62p0` | data/01-bell-and-teleport |
| 21-qubit chain: success after 1 hop | 100% | 93.1% | 94.0% | ibm_marrakesh | `dc2o5teq4uuc73a5lbkg` | data/15-zeno-and-teleportation-chain |
| 21-qubit chain: success after 10 hops | 100% | 58.3% | 58.9% | ibm_marrakesh | `dc2o5teq4uuc73a5lbkg` | data/15-zeno-and-teleportation-chain |

One hop beat 85.4%, the best any classical copy strategy can do for these test states. The chain results were pre-registered. All numbers come from the open dataset https://doi.org/10.5281/zenodo.24517586; see the Twin Check notebook to load and check them.

## Questions and answers
1. **What is the probability that the message qubit (RY(pi/3) on |0>) reads 1?**
   *Answer:* sin^2(pi/6) = 0.25.
2. **After running, how often is the leftmost bit (qubit 2) a 1?**
   *Answer:* About 25% on the ideal device, matching the original message.
3. **Delete the two if-statements and run again. What changes, and why?**
   *Answer:* Qubit 2 reads 1 about 50% of the time: without corrections Bob's qubit is random.
4. **Why can't teleportation send messages faster than light?**
   *Answer:* Bob cannot finish without Alice's two classical bits, which travel at or below light speed.

---
Lawrence AI Solutions · Independent project, not affiliated with or endorsed by IBM. Real-hardware results are from IBM Quantum processors; model predictions are labelled as such.
