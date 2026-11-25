# The quantum Zeno effect: a watched qubit never flips: teacher guide
**Level:** Intermediate (ages 15+) · **Time:** about 35 minutes · From the LAS-Q1 open lesson pack (CC BY 4.0)

Turn a qubit from 0 to 1 in small steps, but look at it after every step. The more often you look, the more it stays at 0.

## Learning goals
- Describe what a measurement does to a qubit partway through a rotation.
- Predict the "stayed at 0" probability for N looks.
- Compare an ideal formula with noisy real-hardware data.

## Background for the teacher
An RY(pi/N) gate turns a qubit a little way from 0 towards 1. If you measure after each of N small turns, each measurement "resets" the qubit to 0 with probability cos^2(pi/2N), so it stays at 0 every time with probability cos^(2N)(pi/2N). As N grows this approaches 1: frequent watching freezes the state (the quantum Zeno effect). The same data is the Elitzur-Vaidman "bomb tester": each look is a bomb that explodes if it finds 1, and "stayed at 0 every time" means the bomb was detected without exploding (interaction-free measurement).

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

## Questions and answers
1. **With no looks in between, where does the full rotation (N steps of pi/N) leave the qubit?**
   *Answer:* At 1: N rotations of pi/N add up to pi, a full flip from 0 to 1.
2. **Use cos^(2N)(pi/2N) to predict "stayed at 0" for N = 2 and N = 10.**
   *Answer:* N = 2: cos^4(45 degrees) = 0.25. N = 10: cos^20(9 degrees) = 0.78.
3. **On the real chip, N = 20 stayed at 0 only 80.8% of the time instead of 88.4%. Why?**
   *Answer:* Every measurement and gate adds a little error, and 20 looks means 20 chances for error; real hardware cannot watch perfectly.
4. **Why does this count as "seeing without looking" in the bomb-tester version?**
   *Answer:* When the qubit stays at 0, the bomb was never triggered, yet the pattern of results tells you a bomb (a measurement) was there.

---
Lawrence AI Solutions · Independent project, not affiliated with or endorsed by IBM. Real-hardware results are from IBM Quantum processors; model predictions are labelled as such.
