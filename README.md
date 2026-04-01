#Project testing using OIDC in Github action
- OIDC
  OpenID Connect (OIDC)  a method offers a more secure way to authenticate GitHub Actions with AWS.
  > using shorlive token from github
  > This token allows GitHub to assume an IAM role temporarily, limiting the scope and duration of AWS access.
- How to
  1) create Identinty Provider in AWS
      > OpenID Connect
      > Provider URL, enter: https://token.actions.githubusercontent.com
      > For Audience, enter: sts.amazonaws.com
  3) create role & attach role you need
  4) Setting on Workflow yaml
     - name: Configure AWS credentials via OIDC
        uses: aws-actions/configure-aws-credentials@v4
         with:
          role-to-assume: "arn:aws:iam::434605749312:role/GitHubOIDCRole"
          aws-region: "ap-south-1"
 
- Troubleshoot
  1) Check openID provider 
     $ aws iam list-open-id-connect-providers
  2) check attach role
    $ aws iam list-attached-role-policies --role-name GitHubOIDCRoleS3
  3) check assumeRoleDocume
    $ aws iam get-role --role-name GitHubOIDCRoleS3
    "StringLike": {
        "token.actions.githubusercontent.com:sub": [
             "repo:resaputra23/PackerAMIAWS:ref:refs/heads/master",      # this must according your repository
             "repo:resaputra23/PackerAMIAWS:ref:refs/heads/master"
         ]
    
