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

We use Jenkins for CI/CD.

Pipeline stages include:
1. Code checkout from repository
2. Build using Maven
3. Run unit tests
4. Build Docker image
5. Push image to container registry
6. Deploy to respective environment

PR vs Merge:
- Pull Requests trigger only build and test stages
- Merge to branches triggers deployment
  
## Rollback Strategy

We maintain versioned Docker images.

If deployment fails:
- The system automatically rolls back to the last stable version
- Health checks are used to detect failures
  
## Configuration Management

We use environment-specific configuration files:

- application-qa.yml
- application-staging.yml
- application-prod.yml

Configurations are injected using environment variables

## Secrets Handling
Sensitive data such as MongoDB credentials and API keys are stored securely using:

- GCP Secret Manager
- Jenkins credentials store

No secrets are hardcoded in the application

## Deployment Strategy
We use Rolling Deployment strategy.

- Application instances are updated one by one
- Ensures zero downtime
- Safer and suitable for small-scale systems

# Infrastructure Design

## Compute
We use Google Cloud Run for deployment.

- Fully managed service
- Auto-scaling based on traffic
- Cost-effective for startups
  
## Database

We use MongoDB Atlas as the database.

- Managed service
- High availability
- No operational overhead
  
## Networking

- Use VPC for secure communication
- Use Load Balancer for routing traffic
- Restrict direct public access to services
  
## IAM & Security

- Use service accounts for applications
- Follow least privilege principle
- Assign minimal required permissions
  
## Logging & Monitoring

- Use GCP Logging for log collection
- Use GCP Monitoring for metrics
- Configure alerts for failures and performance issues
  
