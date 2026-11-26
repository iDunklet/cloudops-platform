# GitHub OIDC Security Design

## 1. Purpose

We use OpenID Connect (OIDC) to improve the security of our CI/CD pipelines. Instead of storing permanent AWS access keys in GitHub, workflows can request temporary AWS credentials. This reduces the risks associated with long-lived credentials.

## 2. Trust Policy

Our production IAM trust policy is restricted to the `iDunklet/cloudops-platform` repository and the `prod` GitHub Environment.

The `dev` environment will use a separate IAM role and trust policy when we implement development deployments. This separation helps prevent development workflows from accessing production resources.

## 3. Permissions Policy

We follow the principle of least privilege. Each IAM role should receive only the permissions required to perform its specific tasks.

We avoid granting administrator permissions to deployment roles because excessive permissions increase the potential impact of a security breach.

## 4. Security Limitations

OIDC provides secure identity federation, but it does not guarantee that workflow code is trustworthy.

We must also protect our branches, review workflow changes, configure environment protections, and monitor AWS activity. These controls work together to reduce security risks.