# Elastic Container Registry (ECR) on AWS

## New AWS Account

- Create an AWS account using these instructions - https://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/
  - Remember to select Basic Support Plan only for now
  - Save your root credentials in a safe location, for e.g in a password manager like 1Password or LastPass
- After creating the account, setup MFA on your root account - https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html#enable-virt-mfa-for-root

## IAM Setup

- Once the root user and account is setup, setup Administrator User and Group - https://docs.aws.amazon.com/IAM/latest/UserGuide/getting-started_create-admin-group.html
- Create two additional groups and attach the respective ECR policies
  - Developer or Poweruser
    - Attach the `AmazonEC2ContainerRegistryFullAccess` Policy
  - ECRUser
    - Attach the `AmazonEC2ContainerRegistryReadOnly` Policy
- Create users and add those users to the groups created above - https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html#id_users_create_console
  - Skip Permissions Boundary when creating new users (not required for now)

## User Login and AWS CLI Setup

- Once the users have been created, they should be able to login with their temporary passwords.
  - Install AWS CLI - https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html
  - Create Access Keys to use AWS CLI - https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-quickstart.html#cli-configure-quickstart-creds
  - Configure your local AWS credentials using the keys created in the step above - https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html
- If your AWS CLI setup was successful, you should be able to run `aws sts get-caller-identity` and the output should look like this:

```json
{
  "UserId": "AJLKAJ2JHJH2342",
  "Account": "7987289479",
  "Arn": "arn:aws:iam::7987289479:user/my_username"
}
```

## ECR Login and Docker Push

- Using AWS CLI and Docker to push your images to ECR - https://docs.aws.amazon.com/AmazonECR/latest/userguide/getting-started-cli.html
