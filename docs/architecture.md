# SupplyChain Sentinel – System Architecture

## 1. Introduction:
SupplyChain Sentinel is designed as a modular software supply chain security platform that integrates dependency analysis, SBOM generation, vulnerability assessment, artifact verification, and security policy enforcement.
The architecture follows a pipeline-based approach in which software components are examined before a release is approved.

## 2. High-Level Architecture:
The platform consists of the following major components:

### 2.1 Source Repository
The source repository contains application code, dependency manifests, lockfiles, and configuration files.

### 2.2 CI/CD Orchestration
GitHub Actions will coordinate the automated security workflow whenever relevant source changes are submitted.

### 2.3 Dependency Analysis Engine
OSV-Scanner and other supported security tools will inspect application dependencies for known vulnerabilities.

### 2.4 SBOM Management Engine
Syft will generate Software Bills of Materials in CycloneDX and SPDX formats to establish a structured inventory of software components.

### 2.5 Vulnerability Analysis Engine
Grype and OSV-Scanner results will be collected and normalized to support vulnerability assessment.

### 2.6 Artifact Integrity Verification
Cosign will be used to sign and verify software artifacts. GitHub artifact attestations will provide additional build provenance evidence.

### 2.7 Security Policy Engine
The custom Python policy engine will evaluate vulnerability findings, artifact verification results, and configured security requirements.
The engine will produce a security decision such as PASS, WARNING, or BLOCK.

### 2.8 Security Dashboard
The dashboard will present dependency information, vulnerability findings, SBOM summaries, integrity verification results, and policy decisions.

## 3. Data Flow:
The proposed data flow is:
1. Developer submits source code.
2. GitHub Actions initiates the security workflow.
3. Dependency analysis identifies application components.
4. SBOM generation creates component inventories.
5. Vulnerability scanners evaluate known security weaknesses.
6. Artifact verification checks signatures and provenance.
7. The policy engine evaluates security requirements.
8. Results are collected for dashboard visualization and reporting.

## 4. Security Design Principles:
The platform will follow these principles:

- Least-privilege access.
- Secure CI/CD workflow permissions.
- Dependency transparency.
- Cryptographic artifact integrity.
- Verifiable build provenance.
- Configurable security policies.
- Evidence-based security decisions.
- Secure handling of credentials and sensitive data.

## 5. Design Limitations:
Vulnerability scanners identify known vulnerabilities but cannot guarantee that every malicious or compromised software component will be detected.
Artifact signatures establish integrity and authenticity relative to a trusted signing identity; they do not independently prove that an artifact is secure.
Build provenance provides evidence about the build process but must be evaluated against an established trust policy.

## 6. Implementation Status:
This document describes the proposed architecture. Individual components will be marked as implemented only after development and successful testing.

**Project:** SupplyChain Sentinel

**Domain:** Software Supply Chain Security and DevSecOps
