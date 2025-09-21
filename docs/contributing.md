# Contributing Guidelines

Thank you for your interest in contributing to the Quantum FaaS Templates repository! This document provides guidelines for contributing new quantum computing templates and improvements.

## How to Contribute

### Adding New Templates

1. **Fork and Clone**
   ```bash
   git fork https://github.com/jayendranarumugam/qfaas-templates.git
   git clone https://github.com/YOUR_USERNAME/qfaas-templates.git
   ```

2. **Create a Branch**
   ```bash
   git checkout -b add-template-[runtime]-[use-case]
   ```

3. **Follow Template Structure**
   - Use existing templates as reference
   - Follow the directory structure: `templates/[quantum-framework]/`
   - Include all required files: `Dockerfile`, `index.py`, `template.yml`, `requirements.txt`

4. **Test Your Template**
   - Ensure the template deploys successfully
   - Test all functionality
   - Add appropriate tests

5. **Submit Pull Request**
   - Provide clear description
   - Include deployment verification
   - Reference any related issues

### Quantum Computing Frameworks

When adding templates, use these quantum computing frameworks:

- `qiskit` - IBM Qiskit for quantum computing
- `cirq` - Google Cirq for quantum computing  
- `braket` - AWS Braket for quantum computing
- `qsharp` - Microsoft Q# for quantum computing
- `pennylane` - Xanadu PennyLane for quantum machine learning
- `forest` - Rigetti Forest for quantum computing

### Quality Standards

All quantum templates must meet these requirements:

- ✅ Include OpenFaaS-compatible `Dockerfile`
- ✅ Provide working quantum algorithm in `index.py`
- ✅ Include `template.yml` with proper configuration
- ✅ List all dependencies in `requirements.txt`
- ✅ Follow quantum computing best practices
- ✅ Include error handling for quantum operations
- ✅ Use consistent naming conventions
- ✅ Test with OpenFaaS CLI

### Code Review Process

1. Manual review by maintainers
2. Testing of quantum function execution
3. OpenFaaS deployment verification
4. Documentation review
5. Approval and merge

### Reporting Issues

When reporting issues:

- Use clear, descriptive titles
- Provide reproduction steps
- Include environment details
- Attach relevant logs/screenshots

### Questions?

- Open an issue for general questions
- Check existing documentation
- Review similar templates for patterns

## Code of Conduct

Please be respectful and constructive in all interactions. We're building this together!