# Kubectl

# Installation

First, you need to download the Kubectl binary from the official Kubernetes release repository. To do this, run the following command in your terminal:


```bash
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
```

This will download the latest stable Kubectl binary from the repository. If you would like to download a specific version instead, you can specify the version in the download URL.

```bash
chmod +x kubectl
```

Run the following command to move the binary to a directory included in the system's PATH environment variable:

```bash
sudo mv kubectl /usr/local/bin
```