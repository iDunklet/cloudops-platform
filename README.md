# ☁️ CloudOps Platform

**A DevOps engineering project focused on AWS Infrastructure as Code, CI/CD automation, and secure cloud deployments.**

## 📌 Project Overview

CloudOps Platform is a hands-on project designed to explore how production-oriented cloud infrastructure can be managed using modern DevOps practices.

The project focuses on building a secure deployment workflow with **AWS CloudFormation, GitHub Actions, OpenID Connect (OIDC), and AWS IAM**.

The objective is to automate infrastructure delivery while applying principles such as least privilege, environment isolation, infrastructure validation, and controlled deployments.

> **Project status:** In active development. CI validation and deployment simulation are implemented. AWS deployment permissions and OIDC integration are currently being designed.

## 🏗️ Architecture

The planned deployment architecture separates authentication, deployment authorization, and infrastructure execution.

```text
Developer
    |
    v
GitHub Pull Request
    |
    v
GitHub Actions CI
    |
    +-- CloudFormation validation
    +-- Protected main branch
    |
    v
GitHub Environment (dev / prod)
    |
    v
GitHub OIDC
    |
    v
AWS Deployment IAM Role
    |
    +-- CloudFormation permissions
    +-- Restricted iam:PassRole
    |
    v
CloudFormation Execution Role
    |
    v
AWS DynamoDB
```

**Current implementation:** The CI validation workflow and manual deployment simulation are functional. The AWS authentication and execution-role components are under development.

## 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| AWS CloudFormation | Infrastructure as Code |
| AWS DynamoDB | Serverless database infrastructure |
| GitHub Actions | CI/CD automation |
| GitHub Environments | Development and production deployment separation |
| AWS IAM | Role-based access control |
| OpenID Connect | Temporary credential federation |
| Python / cfn-lint | Infrastructure validation |
| Git / GitHub | Version control and pull-request workflow |

## ✅ Implemented Features

- CloudFormation template defining a DynamoDB table
- Development and production environment parameters
- DynamoDB retention policies
- Automated CloudFormation linting with GitHub Actions
- Pull-request validation and protected main branch
- GitHub Actions permissions restricted for CI
- Workflow concurrency controls and job timeouts
- Manual deployment simulation using GitHub Actions
- Separate GitHub Environments for development and production
- Production deployment branch restrictions

## 🚧 Work in Progress

- GitHub OIDC authentication with AWS
- Separate development and production IAM deployment roles
- CloudFormation execution roles
- Least-privilege permissions and restricted `iam:PassRole`
- Real AWS infrastructure deployment
- CloudWatch monitoring and alarms
- Deployment rollback and incident-response procedures

## 🔐 Security Design

Security is a core part of the project.

The architecture is designed around the following principles:

**Least privilege:** IAM roles should receive only the permissions necessary to perform their responsibilities.

**Separation of duties:** GitHub deployment roles initiate CloudFormation operations, while dedicated execution roles manage AWS resources.

**Environment isolation:** Development and production deployments use separate identities and permissions.

**Temporary credentials:** GitHub OIDC is intended to replace permanent AWS credentials in deployment workflows.

**Defense in depth:** Branch protection, environment restrictions, IAM policies, and workflow reviews provide complementary security controls.

See [OIDC Security Design](docs/oidc-security-design.md) for additional details.

## 📂 Repository Structure

```text
cloudops-platform/
├── app/
├── infrastructure/
│   ├── template.yaml
│   └── iam/
├── .github/
│   └── workflows/
│       ├── validate-infrastructure.yaml
│       └── deploy-infrastructure.yaml
├── docs/
└── README.md
```

## 🔄 CI/CD Workflow

### Continuous Integration

When changes are pushed to the main branch or submitted through a pull request, GitHub Actions runs CloudFormation validation.

The validation workflow:

1. Checks out the repository.
2. Configures Python.
3. Installs a pinned version of `cfn-lint`.
4. Validates the CloudFormation template.
5. Reports success or failure.

### Deployment Workflow

The deployment workflow can be started manually and allows selection of the `dev` or `prod` environment.

Currently, this workflow **simulates deployment without creating AWS resources**.

Future development will integrate GitHub OIDC and CloudFormation deployment roles.

## 🎯 Learning Objectives

This project is being developed to strengthen practical skills in:

- AWS infrastructure automation
- Secure CI/CD pipeline design
- IAM and least-privilege access
- CloudFormation deployment management
- Environment isolation
- Monitoring and incident response
- DevOps engineering best practices

It also supports preparation for the **AWS Certified DevOps Engineer – Professional (DOP-C02)** certification.

## 📈 Roadmap

- [x] Create the CloudFormation infrastructure template
- [x] Implement automated infrastructure validation
- [x] Configure branch protection and pull-request checks
- [x] Implement manual deployment simulation
- [x] Configure GitHub development and production environments
- [x] Document the initial OIDC security design
- [ ] Complete IAM policy design and review
- [ ] Configure GitHub OIDC federation in AWS
- [ ] Deploy infrastructure through GitHub Actions
- [ ] Implement monitoring and CloudWatch alarms
- [ ] Add rollback and incident-response procedures

## 📖 Project Approach

This repository is developed incrementally, with an emphasis on understanding the purpose of each infrastructure component and the security implications of engineering decisions.

The goal is not only to automate deployments, but to understand how to design, validate, secure, and operate cloud infrastructure responsibly.

---

**Status:** Active development | **Primary AWS Region:** `eu-north-1`