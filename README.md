# Quantum FaaS Templates

A collection of OpenFaaS templates for quantum computing frameworks, enabling serverless quantum function deployment.

## 🚀 Quick Start

```bash
# Clone the repository
git clone https://github.com/jayendranarumugam/qfaas-templates.git
cd qfaas-templates

# Use a template
cp -r templates/qiskit my-quantum-function
cd my-quantum-function

# Deploy with OpenFaaS
faas-cli build -f template.yml
faas-cli deploy -f template.yml
```

## 📁 Repository Structure

```
qfaas-templates/
├── templates/                 # Quantum FaaS templates
│   ├── qiskit/               # IBM Qiskit template
│   ├── cirq/                 # Google Cirq template
│   ├── braket/               # AWS Braket template
│   └── qsharp/               # Microsoft Q# template
├── docker/                   # Docker base images
│   └── base_image/           # Custom base images for each framework
│       ├── qiskit/           # Qiskit base image
│       ├── cirq/             # Cirq base image
│       ├── braket/           # Braket base image
│       └── qsharp/           # Q# base image
├── docs/                     # Documentation
│   ├── getting-started.md    # Quick start guide
│   ├── contributing.md       # Contribution guidelines
│   ├── quantum-frameworks.md # Framework overview
│   └── docker-images.md      # Docker base images guide
├── examples/                 # Usage examples
└── scripts/                  # Utility scripts
```

## 🔬 Supported Quantum Frameworks

| Framework | Provider | Docker Base Image | Template Path |
|-----------|----------|-------------------|---------------|
| **Qiskit** | IBM | `python:3.9.10-slim-bullseye` | `templates/qiskit/` |
| **Cirq** | Google | `python:3.9.10-slim-bullseye` | `templates/cirq/` |
| **Braket** | AWS | `python:3.10-slim-bullseye` | `templates/braket/` |
| **Q#** | Microsoft | `mcr.microsoft.com/quantum/iqsharp-base:latest` | `templates/qsharp/` |

## 🛠️ Prerequisites

- [OpenFaaS CLI](https://docs.openfaas.com/cli/install/)
- [Docker](https://docs.docker.com/get-docker/)
- Python 3.8+
- Quantum computing libraries (installed via requirements.txt)

## 📋 Template Structure

Each template follows a consistent OpenFaaS structure with optimized Docker base images:

```
template-name/
├── Dockerfile          # Container with quantum framework base image
├── index.py           # Main quantum function handler
├── template.yml       # OpenFaaS function configuration
├── requirements.txt   # Additional Python dependencies
└── function/          # Additional function code (Q# only)
```

### 🐳 Docker Base Images

All templates use carefully selected base images with pre-installed quantum libraries:

- **Qiskit**: Custom image with Qiskit 1.4.1 and Python 3.10
- **Cirq**: Custom Cirq image with latest libraries
- **Braket**: Python 3.10 slim with Braket SDK
- **Q#**: Microsoft's official IQ# base image

Custom base images are available in `docker/base_image/` for building your own versions.

## 🚀 Usage Examples

### Qiskit Example
```python
# templates/qiskit/index.py
from qiskit import QuantumCircuit, execute, Aer

def handle(req):
    # Create a simple quantum circuit
    qc = QuantumCircuit(2, 2)
    qc.h(0)
    qc.cx(0, 1)
    qc.measure_all()
    
    # Execute on simulator
    backend = Aer.get_backend('qasm_simulator')
    job = execute(qc, backend, shots=1024)
    result = job.result()
    
    return str(result.get_counts())
```

### Deployment
```bash
# Build and deploy
faas-cli build -f template.yml
faas-cli deploy -f template.yml

# Test the function
echo '{}' | faas-cli invoke my-quantum-function
```

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](docs/contributing.md) for details.

### Adding New Templates

1. Fork the repository
2. Create a new template directory under `templates/`
3. Follow the standard template structure
4. Test with OpenFaaS CLI
5. Submit a pull request

## 📚 Documentation

- [Getting Started](docs/getting-started.md) - Quick start guide
- [Contributing](docs/contributing.md) - How to contribute
- [Quantum Frameworks](docs/quantum-frameworks.md) - Framework overview
- [Docker Base Images](docs/docker-images.md) - Docker configuration guide

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- OpenFaaS community for the serverless platform
- Quantum computing framework maintainers
- Contributors to this template collection