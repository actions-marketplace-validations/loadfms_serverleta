# Serverleta

This Github action compares CloudFormation plans generated by Serverless projects and posts the difference results as a comment in the Pull Requests.

## Inputs

| Inputs         | Description                                                        | Required | Default |
|----------------|--------------------------------------------------------------------|----------|---------|
| s3             | S3 bucket where serverless-state will be stored.                   | True     | ''      |
| build          | Command to build the application.                       | False    | ''      |
| aws_access_key_id | AWS access key to download/upload the latest CloudFormation.           | True     | ''      |
| aws_secret_access_key | AWS secret access key to download/upload the latest CloudFormation. | True     | ''     |
| aws_region | AWS S3 region. | True     | ''     |
| github_token   | Github token to write comments in PR.                             | True     | ''      |
| generate_comment | Whether to generate a comment or not.                | False    | 'true'  |
| generate_cloudformation | Whether to generate and save the CloudFormation or not. | False    | 'false' |

## Usage

### Save current state in s3

On your deploy action add these lines:
```yaml
    - name: serverleta
      uses: loadfms/serverleta@v1.0.8
      with:
        s3: "s3-bucket-name/repo-name"
        build: "make build-command"
        aws_access_key_id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws_secret_access_key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws_region: "sa-east-1"
        github_token: ${{ secrets.TOKEN }}
        generate_comment: "false" 
        generate_cloudformation: "true"

```

### Add comment with plan

On your pull request action add these lines:
```yaml
    - name: serverleta
      uses: loadfms/serverleta@v1.0.8
      with:
        s3: "s3-bucket-name/repo-name"
        build: "make build-command"
        aws_access_key_id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws_secret_access_key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws_region: "sa-east-1"
        github_token: ${{ secrets.TOKEN }}
        generate_comment: "true" 
        generate_cloudformation: "false"

```
