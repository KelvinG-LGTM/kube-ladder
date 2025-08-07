# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is "kube-ladder" - a comprehensive Kubernetes learning path repository maintained by Caicloud. It's a structured curriculum designed to guide learners through 7 progressive stages of Kubernetes mastery, from basic installation to advanced concepts and ecosystem projects.

The repository is primarily educational content written in Chinese, organized as a progressive learning ladder with hands-on tutorials and YAML resource examples.

## Repository Structure

The repository consists of:

- **Root**: README.md with the complete learning curriculum, OWNERS file
- **tutorials/**: Step-by-step lab guides and learning materials
  - `lab1-installation.md` - Installation guide (minikube, kind, manual setup)
  - `lab2-application-and-service.md` - Basic concepts (Pods, Services, Labels)
  - `lab3-manual-installtion.md` - Manual cluster installation
  - `lab4-concepts.md` - Advanced concepts and features
  - `images/` - Supporting diagrams and screenshots
  - `resources/` - YAML manifests and configuration files
- **tutorials/resources/**: Example Kubernetes manifests
  - Core resource examples: pod.yaml, deployment_nginx.yaml, etc.
  - Advanced examples: job.yaml, cronjob.yaml, daemonset.yaml
  - Storage examples: pv_hostpath.yaml, pvc.yaml
  - Network examples: kube-flannel.yaml, coredns.yaml
  - Configuration examples: pod_configmap.yaml, quota.yaml

## Working with YAML Files

When modifying Kubernetes YAML files in `tutorials/resources/`:

- Maintain proper YAML formatting and indentation
- Follow Kubernetes API conventions for resource definitions
- Use appropriate namespaces (many examples use `tutorial` namespace)
- Resource requests/limits should be realistic for learning environments
- Image references should use stable tags or `latest` for demo purposes

## Common Tasks

Since this is a documentation/tutorial repository, common tasks include:

- **Updating tutorial content**: Edit markdown files in `tutorials/`
- **Modifying YAML examples**: Update resource definitions in `tutorials/resources/`
- **Adding new examples**: Create new YAML files following existing naming patterns
- **Updating learning paths**: Modify README.md sections for curriculum changes

## Testing and Validation

This is primarily a documentation repository with no build system or automated tests. However:

- YAML files should be syntactically valid
- Kubernetes manifest files should conform to API schemas
- Tutorial instructions should be accurate for supported Kubernetes versions
- Links in documentation should be functional

## Notes for Development

- The content is primarily in Chinese - maintain language consistency
- The repository follows a structured learning progression (7 stages)
- YAML examples are designed for learning, not production use
- Some files show modifications in git status - likely from tutorial exercises
- The project uses semantic file organization by learning stage and concept type