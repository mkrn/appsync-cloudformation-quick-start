# AWS AppSync CloudFormation Quick Start Template

### Bootstrap
1) Launching bootstrap.yaml CloudFormation template on your account:

- Review and adjust bootstrap.yaml if necessary
- Replace [PROJECT_NAME] with lowercase project name
- Fill in [GITHUB_USERNAME] [GITHUB_REPOSITORY_NAME] [GITUB_TOKEN]
- Run
- Check Cloudformation to make sure it launched properly

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
  GitHubToken=[GITUB_TOKEN]
```

2) Creating your first user in Cognito user pool

```
aws cognito-idp sign-up   \
  --profile test  \
  --region us-west-2 \
  --client-id 6vk51is4s290c86lrsvvs43spc \
  --username 18294541696 \
  --password testTest12#$ \
  --user-attributes Name=email,Value=ffab00@gmail.com Name=phone_number,Value=+18294541696 &&
aws cognito-idp admin-set-user-settings   \
  --profile test  \
  --region us-west-2 \
  --user-pool-id us-west-2_XjenccFei \
  --username 18294541696 \
  --mfa-options DeliveryMedium=SMS,AttributeName=phone_number
```

### Resources

- CI Pipeline (CodePipeline)
- Build Service (CodeBuild)
- RDS Postgres Database Instance
- Security Group opening port 5432 for outside access
- User Pool (Cognito)
- Identity Pool
- User Pool client
- Authenticated and Unauthenticated user roles
- S3 Bucket for lambda and CloudFormation uploads

Once bootstrap stack it checks out the project code from repository, builds and uploads Lambda-resolver code and launces iac.yaml stack and creates:

- AppSync API project
- AppSync Schema
- Lambda
- AppSync DataSource
- AppSync Resolvers


## TODO

- [x] Add RDS option to bootstrap
- [x] Add Cognito Userpool to bootstrap
- [ ] Tests for Lambda
- [ ] eslint for Lambda
- [ ] pre-commit checks
- [ ] Version with knex
- [ ] Add VPC to bootstrap, connect RDS & Lambda into it
- [ ] Yeoman create new resolver (in iac, lambda js file)
- [ ] Test data-loader in loader.js
- [ ] GraphQL Voyager

## License

MIT
