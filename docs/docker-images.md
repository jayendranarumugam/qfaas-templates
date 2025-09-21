# Docker Base Images

This document describes the Docker base images used for each quantum computing framework template in this repository.

## Overview

Each quantum FaaS template uses carefully selected Docker base images that include the necessary quantum computing libraries and dependencies. The templates also include custom base images in the `docker/base_image/` directory for reference and rebuilding purposes.

## Base Images by Framework

### Qiskit Template

**Template Base Image:** `python:3.9.10-slim-bullseye` 
- **Custom Base Image Location:** `docker/base_image/qiskit/`
- **Python Version:** 3.10
- **Qiskit Version:** 1.4.1
- **Features:**
  - Pre-installed Qiskit with all core modules
  - Optimized for quantum circuit simulation
  - Compatible with IBM Quantum backends

### Cirq Template

**Template Base Image:** `python:3.9.10-slim-bullseye`
- **Custom Base Image Location:** `docker/base_image/cirq/`
- **Python Version:** 3.9+
- **Features:**
  - Complete Cirq installation
  - Google Quantum AI compatibility
  - TensorFlow Quantum integration ready

### AWS Braket Template

**Template Base Image:** `python:3.10-slim-bullseye`
- **Custom Base Image Location:** `docker/base_image/braket/`
- **Python Version:** 3.10
- **Features:**
  - Amazon Braket SDK
  - AWS integration capabilities
  - Multi-backend quantum execution

### Microsoft Q# Template

**Template Base Image:** `mcr.microsoft.com/quantum/iqsharp-base:latest`
- **Custom Base Image Location:** `docker/base_image/qsharp/`
- **Features:**
  - Q# language support
  - IQ# Jupyter kernel
  - Azure Quantum integration
  - .NET quantum runtime

## Docker Architecture

All templates follow this multi-stage Docker build pattern:

```dockerfile
# Stage 1: Get OpenFaaS watchdog
FROM ghcr.io/openfaas/of-watchdog:0.9.11 as watchdog

# Stage 2: Use quantum framework base image
FROM [quantum-framework-base-image]

# Copy watchdog and set permissions
COPY --from=watchdog /fwatchdog /usr/bin/fwatchdog
RUN chmod +x /usr/bin/fwatchdog

# Framework-specific setup
# ... additional configuration
```

## Custom Base Images

The `docker/base_image/` directory contains Dockerfiles for building custom base images:

```
docker/base_image/
├── qiskit/
│   └── Dockerfile      # Custom Qiskit base image
├── cirq/
│   └── Dockerfile      # Custom Cirq base image
├── braket/
│   └── Dockerfile      # Custom Braket base image
└── qsharp/
    └── Dockerfile      # Custom Q# base image
```

### Building Custom Base Images

To build your own custom base image:

```bash
# Build Qiskit base image
cd docker/base_image/qiskit
docker build -t your-registry/qiskit-base:latest .

# Build Cirq base image  
cd docker/base_image/cirq
docker build -t your-registry/cirq-base:latest .
```

Then update the template's Dockerfile to use your custom image: in `template/<template-name>/Dockerfile`
```dockerfile
FROM your-registry/qiskit-base:latest
```

### Using the Templates

The templates are preconfigured to work with custom base images. To use them:

1. **Build the base images** (or use your own registry images)
2. **Update Dockerfiles** in templates to reference your images
3. **Build and deploy** with OpenFaaS CLI

## Image Size Optimization

Our base images are optimized for:
- **Minimal size** - Using slim/alpine variants where possible
- **Fast startup** - Pre-installed quantum libraries
- **Security** - Non-root user execution
- **Caching** - Efficient layer ordering

## Version Management

| Framework | Current Version | Update Policy |
|-----------|----------------|---------------|
| Qiskit | 1.4.1 | Follow Qiskit releases |
| Cirq | Latest | Use stable releases |
| Braket | SDK via pip | Latest compatible |
| Q# | IQ# Latest | Follow Microsoft releases |

## Building Templates

When building templates, Docker will:
1. Pull the quantum framework base image
2. Copy application code
3. Install additional dependencies from `requirements.txt`
4. Configure OpenFaaS watchdog

Build command:
```bash
faas-cli build -f template.yml
```

## Troubleshooting

### Common Issues

1. **Large Image Size**
   - Use multi-stage builds
   - Clean package caches
   - Minimize installed packages

2. **Slow Builds**
   - Leverage Docker layer caching
   - Pre-build custom base images
   - Use .dockerignore files

3. **Runtime Errors**
   - Check quantum library versions
   - Verify Python compatibility
   - Review resource limits

### Debugging

To debug a template image:
```bash
docker run -it [image-name] /bin/bash
```

## Best Practices

1. **Pin specific versions** for reproducible builds
2. **Use multi-stage builds** to reduce final image size
3. **Run as non-root user** for security
4. **Clean up package managers** to reduce size
5. **Test locally** before deploying

## Contributing

When adding new quantum frameworks:
1. Create custom base image in `docker/base_image/[framework]/`
2. Update template Dockerfile to use the base image
3. Document image details in this file
4. Test build and deployment process