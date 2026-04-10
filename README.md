<div align="center">

# ⚛️ Quantum Computing — Educational Research Repository

**Educational notes, quantum circuits, and hands-on examples built with Qiskit & PennyLane.**

[![Jupyter Book](https://img.shields.io/badge/Jupyter%20Book-orange?logo=jupyter&logoColor=white&style=flat-square)](https://jupyterbook.org)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-181717?logo=github&logoColor=white&style=flat-square)](https://pages.github.com)
[![Qiskit](https://img.shields.io/badge/Qiskit-6929C4?logo=ibm&logoColor=white&style=flat-square)](https://qiskit.org)
[![PennyLane](https://img.shields.io/badge/PennyLane-00A3E0?style=flat-square)](https://pennylane.ai)
[![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?logo=python&logoColor=white&style=flat-square)](https://www.python.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)

</div>

---

## 📌 About

This repository is an **educational resource** created to share my research and studies in the field of quantum computing. All content is built around runnable Jupyter Notebooks that combine theoretical background with practical Python examples.

Everything is compiled using **[Jupyter Book](https://jupyterbook.org)** and published via **[GitHub Pages](https://pages.github.com)**.

> **Target audience:** Students, researchers, and software developers who are curious about quantum computing and looking for a solid starting point.

---

## 🔬 Libraries Used

### [Qiskit](https://qiskit.org) — IBM Quantum Framework

Developed by IBM, Qiskit is used throughout this repository for circuit construction, simulation, and accessing real quantum hardware through IBM Quantum.

```python
from qiskit import QuantumCircuit
from qiskit_aer import AerSimulator

# Bell State (Entanglement) example
qc = QuantumCircuit(2, 2)
qc.h(0)        # Hadamard gate → superposition
qc.cx(0, 1)    # CNOT gate → entanglement
qc.measure([0, 1], [0, 1])

simulator = AerSimulator()
result = simulator.run(qc, shots=1024).result()
print(result.get_counts())
# Output: {'00': 512, '11': 512}
```

### [PennyLane](https://pennylane.ai) — Differentiable Quantum Computing

Developed by Xanadu, PennyLane is used for differentiable quantum programming, gradient-based optimization, and Quantum Machine Learning (QML) experiments.

```python
import pennylane as qml
import numpy as np

dev = qml.device("default.qubit", wires=2)

@qml.qnode(dev)
def bell_circuit():
    qml.Hadamard(wires=0)
    qml.CNOT(wires=[0, 1])
    return qml.probs(wires=[0, 1])

print(bell_circuit())
# Output: [0.5, 0.  , 0.  , 0.5]
```

---


## 🌐 Deploying to GitHub Pages

```bash
pip install ghp-import
ghp-import -n -p -f _build/html
```

This pushes the built book to the `gh-pages` branch automatically. Your documentation will then be live at:

```
https://username.github.io/repo-name
```

---

## 🗺️ Roadmap

- [x] *Data–Output Oriented Problem Typology in Quantum Machine Learning*
- [ ] *Data Encoding in Quantum Machine Learning: Theoretical Foundations and Applications*


---

## 🤝 Contributing

Contributions are very welcome! Whether it's a bug report, a content suggestion, or a new notebook — feel free to get involved .In these cases, I would be very happy to see your email.

---

## 📄 License

This project is licensed under the **MIT License**. See the [LICENSE](LICENSE) file for details.

---

## 📬 Contact

For questions, suggestions, or collaboration:

- 🐛 **email:** erns.bzkrt@gmail.com

---

<div align="center">

*Let's explore the quantum world together.* ⚛️

</div>
