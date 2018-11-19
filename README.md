# AWS AppSync CloudFormation Quick Start Template

### Bootstrap
1) Launch bootstrap.yaml CloudFormation template on your account:

- Review and adjust bootstrap.yaml if necessary
- Create personal access token on https://github.com/settings/tokens 
- Replace [PROJECT_NAME] with lowercase project name
- Fill in [GITHUB_USERNAME] [GITHUB_REPOSITORY_NAME] [GITHUB_TOKEN]
- Run
- Check CloudFormation to make sure it launched properly. CodePipeline will be created and run build and deploy iac.yaml template.

```
aws cloudformation deploy \
  --template-file bootstrap.yaml \
  --stack-name [PROJECT_NAME]Bootstrap \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameter-overrides \
  Prefix=[PROJECT_NAME]_[ENVIRONMENT] \
  GithubOwner=[GITHUB_USERNAME]\
  GithubRepo=[GITHUB_REPOSITORY_NAME]\
  GithubBranch=master\
  GitHubToken=[GITHUB_TOKEN]
```

2) Review 

### Creating your first user in Cognito user pool

```
aws cognito-idp sign-up   \
  --region [REGION] \
  --client-id [COGNITO_CLIENT_ID] \
  --username 18... \
  --password somePassword12$$ \
  --user-attributes Name=email,Value=email@gmail.com Name=phone_number,Value=+18..... &&
aws cognito-idp admin-set-user-settings   \
  --region [REGION] \
  --user-pool-id [USER_POOL_ID] \
  --username 18294541696 \
  --mfa-options DeliveryMedium=SMS,AttributeName=phone_number
```

### Resources

- CI Pipeline (CodePipeline)
- Build Service (CodeBuild)
- User Pool (Cognito)
- Identity Pool
- User Pool client
- Authenticated and Unauthenticated user roles
- S3 Bucket for lambda and CloudFormation uploads

Once bootstrap stack it checks out the project code from repository, builds and uploads Lambda-resolver code and launces iac.yaml stack and creates:

- AppSync API project
- AppSync Schema
- AppSync DataSource
- AppSync Resolvers


## TODO

- [ ] Tests for Lambdas
- [ ] eslint for Lambda
- [ ] pre-commit checks
- [ ] GraphQL Voyager
- [ ] Separate GraphQL to a sub-stack so that multiple APIs could be created (one with Cognito auth, other with api key auth)

## License

MIT
