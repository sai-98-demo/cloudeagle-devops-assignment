# CI/CD Design

## Branching Strategy
We follow a simple Git branching strategy:

- feature/* branches for development
- develop branch for QA environment
- staging branch for staging environment
- main branch for production

Each branch is mapped to its respective environment.

To avoid accidental production deployments:
- Only main branch triggers production deployment
- Pull request approval is required before merging
- Manual approval is added before production deployment

## Jenkins Pipeline

## Rollback Strategy

## Configuration Management

## Secrets Handling

## Deployment Strategy


# Infrastructure Design

## Compute

## Database

## Networking

## IAM & Security

## Logging & Monitoring
