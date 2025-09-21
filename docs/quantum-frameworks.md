# Quantum Computing Frameworks

This document provides an overview of the quantum computing frameworks supported in this repository.

## Qiskit (IBM)

**Directory:** `templates/qiskit/`
**Docker Base Image:** `python:3.9.10-slim-bullseye`

Qiskit is IBM's open-source quantum computing framework.

### Key Features
- Circuit-based quantum programming
- Extensive quantum algorithm library
- Integration with IBM Quantum systems
- Quantum machine learning capabilities

### Docker Configuration
- **Base Image:** Custom image built from `docker/base_image/qiskit/`
- **Qiskit Version:** 1.4.1 pre-installed
- **Python Version:** 3.10

### Use Cases
- Quantum algorithms research
- NISQ device programming
- Quantum simulation
- Educational purposes

### Getting Started
```python
from qiskit import QuantumCircuit, execute, Aer

# Create a quantum circuit
qc = QuantumCircuit(2, 2)
qc.h(0)  # Hadamard gate
qc.cx(0, 1)  # CNOT gate
qc.measure_all()
```

## Cirq (Google)

**Directory:** `templates/cirq/`
**Docker Base Image:** `python:3.9.10-slim-bullseye`

Cirq is Google's quantum computing framework for writing, manipulating and optimizing quantum circuits.

### Key Features
- Native support for Google's quantum hardware
- Flexible circuit construction
- Advanced optimization capabilities
- Integration with TensorFlow Quantum

### Docker Configuration
- **Base Image:** Custom image built from `docker/base_image/cirq/`
- **Python Version:** 3.9+
- **Cirq Libraries:** Latest version pre-installed

### Use Cases
- Quantum supremacy experiments
- Variational quantum algorithms
- Quantum machine learning
- Hardware-specific optimizations

### Getting Started
```python
import cirq

# Create qubits and circuit
qubits = cirq.LineQubit.range(2)
circuit = cirq.Circuit()
circuit.append(cirq.H(qubits[0]))
circuit.append(cirq.CNOT(qubits[0], qubits[1]))
```

## AWS Braket

**Directory:** `templates/braket/`
**Docker Base Image:** `python:3.10-slim-bullseye`

AWS Braket provides access to quantum computing hardware from multiple providers.

### Key Features
- Multi-vendor quantum hardware access
- Hybrid classical-quantum algorithms
- Managed Jupyter notebooks
- Integration with AWS services

### Docker Configuration
- **Base Image:** Python 3.10 slim with Braket SDK
- **AWS Integration:** Pre-configured for Braket services
- **Custom Base:** Available in `docker/base_image/braket/`

### Use Cases
- Cross-platform quantum development
- Hybrid algorithms
- Large-scale quantum simulations
- Production quantum applications

### Getting Started
```python
from braket.circuits import Circuit
from braket.devices import LocalSimulator

# Create circuit
circuit = Circuit().h(0).cnot(0, 1)

# Run on local simulator
device = LocalSimulator()
task = device.run(circuit, shots=1000)
```

## Microsoft Q#

**Directory:** `templates/qsharp/`
**Docker Base Image:** `mcr.microsoft.com/quantum/iqsharp-base:latest`

Q# is Microsoft's quantum-focused programming language.

### Key Features
- High-level quantum programming language
- Strong type system for quantum programs
- Integration with .NET ecosystem
- Azure Quantum integration

### Docker Configuration
- **Base Image:** Official Microsoft IQ# base image
- **Q# Runtime:** Pre-installed with Jupyter kernel support
- **Custom Base:** Available in `docker/base_image/qsharp/`

### Use Cases
- Large-scale quantum applications
- Quantum algorithm development
- Resource estimation
- Education and research

### Getting Started
```qsharp
operation HelloQuantum() : Unit {
    use q = Qubit();
    H(q);
    let result = M(q);
    Message($"Measurement result: {result}");
}
```

## Template Structure

Each quantum framework template follows this structure:

```
framework-name/
├── Dockerfile          # Container configuration with base image
├── index.py           # Main function handler
├── template.yml       # OpenFaaS configuration  
├── requirements.txt   # Python dependencies
└── function/          # Additional code (Q# only)
```

### Docker Base Images

All templates use optimized base images with pre-installed quantum libraries:

| Framework | Base Image | Custom Base Location |
|-----------|------------|---------------------|
| Qiskit | `jayendranarumugam/qiskit-py310:1.4.1` | `docker/base_image/qiskit/` |
| Cirq | `quantumdev/cirq:latest` | `docker/base_image/cirq/` |
| Braket | `python:3.10-slim-bullseye` | `docker/base_image/braket/` |
| Q# | `mcr.microsoft.com/quantum/iqsharp-base:latest` | `docker/base_image/qsharp/` |

## Deployment

All templates are designed for OpenFaaS deployment:

```bash
faas-cli build -f template.yml
faas-cli deploy -f template.yml
```

## Performance Considerations

- **Simulation vs Hardware**: Templates work with simulators by default
- **Resource Requirements**: Quantum simulations can be memory intensive
- **Timeout Settings**: Configure appropriate timeouts for complex algorithms
- **Error Handling**: Include proper error handling for quantum operations