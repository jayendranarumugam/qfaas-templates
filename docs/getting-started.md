# Getting Started

This guide will help you quickly get started with using the Quantum FaaS templates in this repository.

## Prerequisites

- Git
- OpenFaaS CLI (`faas-cli`)
- Docker (for building container images)
- Python 3.8+ (for local development)
- Quantum computing libraries (pre-installed in Docker base images)

## Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/jayendranarumugam/qfaas-templates.git
   cd qfaas-templates
   ```

2. **Choose a template**
   Browse the `templates/` directory to find a quantum computing template that matches your needs:
   ```
   templates/
   ├── qiskit/          # IBM Qiskit quantum computing
   ├── cirq/            # Google Cirq quantum computing
   ├── braket/          # AWS Braket quantum computing
   └── qsharp/          # Microsoft Q# quantum computing
   ```

3. **Copy the template**
   ```bash
   cp -r templates/qiskit my-quantum-function
   cd my-quantum-function
   ```

4. **Customize the template**
   - Update the quantum algorithm in `index.py`
   - Modify `requirements.txt` for additional dependencies
   - Update `template.yml` configuration

5. **Deploy with OpenFaaS**
   ```bash
   faas-cli build -f template.yml
   faas-cli deploy -f template.yml
   ```

## Template Structure

Each quantum template follows a consistent OpenFaaS structure:

```
template-name/
├── Dockerfile             # Container with quantum framework base image
├── index.py              # Main quantum function
├── template.yml          # OpenFaaS configuration
├── requirements.txt      # Additional Python dependencies
└── function/             # Additional function code (Q# only)
```

### Docker Base Images

Each template uses optimized Docker base images with pre-installed quantum libraries:

- **Qiskit:** `python:3.9.10-slim-bullseye` + Qiskit SDK 1.4.1
- **Cirq:** `python:3.9.10-slim-bullseye` + Cirq SDK
- **Braket:** `python:3.10-slim-bullseye` + Braket SDK
- **Q#:** `mcr.microsoft.com/quantum/iqsharp-base:latest`

Custom base images are available in `docker/base_image/` for building your own versions.

## Next Steps

- [Contributing Guidelines](contributing.md)
- [Quantum Frameworks Overview](quantum-frameworks.md)
- [Docker Base Images](docker-images.md)