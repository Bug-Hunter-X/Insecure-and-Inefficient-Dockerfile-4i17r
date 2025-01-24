# Insecure and Inefficient Dockerfile
This repository demonstrates a vulnerable and inefficient Dockerfile and its improved version.

## Issues with the Original Dockerfile

* **Insecure Base Image:** Using `ubuntu:latest` is risky.  It pulls the very newest version, which may contain unpatched vulnerabilities.  It's crucial to specify a particular version for reproducible builds and security.
* **Missing Python Version Specifier:**  The Dockerfile omits specifying the Python version.  Inconsistent Python versions across environments can lead to runtime errors.
* **Unoptimized `pip install`:**  The `pip install -r requirements.txt` command lacks optimization. This can lead to larger image sizes, slower builds, and unnecessary dependencies.

## Improved Dockerfile
The `Dockerfile_fixed` provides the corrected and more robust solution. This includes:
* Using a specific, secure base image.
* Specifying Python version.
* Optimizing `pip install` using `--no-cache-dir` to avoid unnecessary caching.
* Creating a minimal image by cleaning up after installs.

## How to reproduce
1. Clone this repository.
2. Build the original Dockerfile: `docker build -t insecure-app .`
3. Build the fixed Dockerfile: `docker build -t secure-app -f Dockerfile_fixed .`
4. Compare the image sizes (docker images).
5. (Optional) Scan the images for vulnerabilities using a tool like Trivy.