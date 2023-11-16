# Overview
Infrastructure for the [Agora](https://github.com/Sage-Bionetworks/Agora)
application.


# Purpose
This repo contains infrastructure templates for the Agora application.
It is also setup with CI/CD to automatically deploy the infrastructure
to AWS.


# Architecture
Agora runs on AWS as an Elastic Beanstalk app.


![alt text][architecture]


## Security
The instances running agora and the database for it runs in a private
subnet which means neither the instances nor the database are accessible
from the internet.

# Workflow
There is a specific workflow for making changes to the infrastructure.
* Make pull requests to this repo
* Get someone to review and approve your changes
* Change is merged after being approved
* Github action runs a build to test the infrastructure templates
* Github action deploys the updated infrastructure to AWS


## Continuous Integration
We have configured Github actions to deploy CF template updates.  GH action
deploys using [sceptre](https://sceptre.cloudreach.com/latest/about.html)


# AWS Infrastructure
We setup Agora application to run in AWS Elastic Beanstalk.  The beanstalk
is setup to run Agora in three environments:
* Development -> https://agora-develop.adknowledgeportal.org
* Staging -> https://agora-staging.adknowledgeportal.org
* Production -> https://agora.adknowledgeportal.org

## Deployment Workflow
To deploy Agora updates to one of the environments just merge code to the branch you would like
to deploy to then GH action will take care of building, testing and deploying the Agora
application.


# Contributions

## Issues
* https://sagebionetworks.jira.com/projects/IT

## Secrets
* We use the [AWS SSM](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-paramstore.html)
to store secrets for this project.  Sceptre retrieves the secrets using
a [sceptre ssm resolver](https://github.com/cloudreach/sceptre/tree/v1/contrib/ssm-resolver)
and passes them to the cloudformation stack on deployment.


[architecture]: infra-arch1.png "Agora architecture"
