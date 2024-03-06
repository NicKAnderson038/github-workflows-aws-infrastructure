# Welcome
This project is intended to be used alongside Myles Loffler's Medium story titled: Using Github Actions to Deploy a CDK Application.

The project structure is reflective of `cdk init app --languge=typescript` and defines two primary things:

 - An OIDC Provider in IAM which will permit GitHub Actions to assume a specific role.
 - A simple Lambda function which will be deployed as an example.

Please see the [Medium story](https://medium.com/@mylesloffler/using-github-actions-to-deploy-a-cdk-application-f28b7f792f12#a16e) as a guide for using the contents of this [repository](https://github.com/myles2007/story-Using-Github-Actions-to-Deploy-a-CDK-Application).

<br/>

## Getting Started

Clone repo and perform an `npm install`

<sub>*Make sure git & node is installed to your system prior.</sub>

<br/>

## Establishing Trust Between Github & AWS

If you have a `default` AWS profile configured and want to deploy to that account and region, you can omit `AWS_PROFILE=<your-profile>`

```bash
# AWS_PROFILE=<your-profile> npx cdk deploy TrustStack --parameters GitHubOrg=<your-org> --parameters GitHubRepo=<your-repo>

npx cdk deploy TrustStack --parameters GitHubOrg=NicKAnderson038 --parameters GitHubRepo=github-workflows-aws-infrastructure
```
<br/>

## Managing Infrastructure with commits

This will Create the trust relationship with aws. And return the `TrustStackGitHubActionsRoleArn` needed for the repository variables in the github repo.

| Name    | Value |
| -------- | ------- |
| AWS_GITHUB_ACTIONS_ROLE  | `<TrustStackGitHubActionsRoleArn>`    |
| AWS_TARGET_REGION | `us-east-1`     |

After that, begin adding the additional infrastructure resources that need to be deployed with in `./bin/example.ts`. The example in this repo would be the `LambdaStack` in `./lib/LambdaStack.ts` and push to github `main` branch. Update `./github/workflows/*.yml` prior to pushing commit to the `main` branch.

Another option is to use newly created `<TrustStackGitHubActionsRoleArn>` for deploying webapp or services to currently running aws instances. This would require updating the `./github/workflows/*.yml` for deploying applications.

<br/>

<sub>Quick link for to my [repository variables](https://github.com/NicKAnderson038/github-workflows-aws-infrastructure/settings/variables/actions) in this repo.</sub>

<sub><sub>`https://github.com/<Your_Github_Account>/<Your_Github_Repo>/variables/actions`</sub></sub>