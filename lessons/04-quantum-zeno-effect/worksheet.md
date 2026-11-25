# The quantum Zeno effect: a watched qubit never flips: student worksheet
Name: ______________________ Date: ____________

Turn a qubit from 0 to 1 in small steps, but look at it after every step. The more often you look, the more it stays at 0.

## Run it yourself (free tools)
- **Quirk** (drag-and-drop simulator in the browser): https://algassert.com/quirk
- **IBM Quantum Composer** (free account; can run on real hardware): https://quantum.cloud.ibm.com/composer
- **Qiskit** (Python, free; works in Google Colab):

```python
from qiskit import QuantumCircuit
import numpy as np
N = 10                       # number of looks; try 1, 2, 3, 5, 10, 20
qc = QuantumCircuit(1, N)
for k in range(N):
    qc.ry(np.pi / N, 0)      # a small turn from 0 towards 1
    qc.measure(0, k)         # look (mid-circuit measurement)
# "stayed at 0 every time" = the all-zeros outcome
```

## What a real quantum computer measured
| Quantity | Perfect computer | Predicted before the run (LAS-Q1) | Real chip | Chip | Job ID | Dataset folder |
|---|---|---|---|---|---|---|
| Stayed at 0, N = 2 looks | 25.0% | 23.9% | 25.1% | ibm_marrakesh | `dc2o5t6q4uuc73a5lbig` | data/15-zeno-and-teleportation-chain |
| Stayed at 0, N = 5 looks | 60.5% | 54.3% | 60.5% | ibm_marrakesh | `dc2o5t6q4uuc73a5lbig` | data/15-zeno-and-teleportation-chain |
| Stayed at 0, N = 10 looks | 78.1% | 73.5% | 76.5% | ibm_marrakesh | `dc2o5t6q4uuc73a5lbig` | data/15-zeno-and-teleportation-chain |
| Stayed at 0, N = 20 looks | 88.4% | 74.3% | 80.8% | ibm_marrakesh | `dc2o5t6q4uuc73a5lbig` | data/15-zeno-and-teleportation-chain |

Pre-registered; both tests passed (watching 20 times beat watching twice, z = 42.5). The model was too pessimistic for many looks, a known weakness we publish. All numbers come from the open dataset https://doi.org/10.5281/zenodo.24517586; see the Twin Check notebook to load and check them.

## Questions
1. With no looks in between, where does the full rotation (N steps of pi/N) leave the qubit?

   ______________________________________________________________

   ______________________________________________________________

2. Use cos^(2N)(pi/2N) to predict "stayed at 0" for N = 2 and N = 10.

   ______________________________________________________________

   ______________________________________________________________

3. On the real chip, N = 20 stayed at 0 only 80.8% of the time instead of 88.4%. Why?

   ______________________________________________________________

   ______________________________________________________________

4. Why does this count as "seeing without looking" in the bomb-tester version?

   ______________________________________________________________

   ______________________________________________________________

---
LAS-Q1 open lesson pack · CC BY 4.0 · Lawrence AI Solutions
