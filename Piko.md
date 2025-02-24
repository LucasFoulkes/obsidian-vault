# Piko Overview

## Introduction
Piko is an open-source reverse proxy designed to provide a secure way to connect to services that are not publicly routable. It serves as an alternative to Ngrok, optimized for production traffic and simple to host, especially on Kubernetes.

## Features
- Secure tunneling for non-public services
- Built for production traffic with clustering and zero-downtime deployments
- Simple hosting behind HTTP(S) load balancer on Kubernetes
- Supports HTTP and TCP connections
- Load balancing and endpoint management

## Installation
You can install Piko via Docker or build it from source:

### Using Docker
```bash
docker pull andydunstall/piko
docker run -p 8000:8000 andydunstall/piko
```

### Building from Source
```bash
git clone https://github.com/andydunstall/piko.git
cd piko
make piko
make image
```

## Basic Usage
Here's a quick example to set up a Piko cluster and register an endpoint:

### Setting up the Cluster
```bash
cd docs/demo
docker compose up
```

### Registering an Endpoint
```bash
piko agent http my-endpoint 4000
```

## Documentation and Resources
- [GitHub Repository](https://github.com/andydunstall/piko)
- [Piko Wiki](https://github.com/andydunstall/piko/wiki)
- [Ngrok](https://ngrok.com/)

## Contributing
Contributions are welcome! Please see the [contributing guidelines](https://github.com/andydunstall/piko/blob/main/CONTRIBUTING.md) for more details.

## License
Piko is licensed under the [MIT License](https://github.com/andydunstall/piko/blob/main/LICENSE).

---

### Explanation:

- **Title:** Clearly states the topic of the note.
- **Introduction:** Summarizes the project's purpose and core functionality.
- **Features:** Highlights key functionalities, making it easier to understand the library's capabilities.
- **Installation:** Provides a quick start guide to install the library, facilitating immediate usage.
- **Basic Usage:** Demonstrates how to use the library with simple examples.
- **Documentation and Resources:** Offers links to additional information and documentation for deeper understanding.
- **Contributing:** Encourages community contributions, ensuring the project can grow and improve.
- **License:** Clarifies the legal usage terms of the library.

This structure ensures that the essential information is organized logically, making it easy for users to find what they need quickly.