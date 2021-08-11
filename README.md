# AWS Lambda Terraform Module for image based lambdas

This module will deploy an image based Lambda function.

## Module Input Variables

- `function_name` - (string) - **REQUIRED** - The name of the Lambda function.
- `image_uri` - (string) - **REQUIRED** - Uri to the image in ECR repo.
- `image_config_command` - (list) - List of values with which to override CMD entry in the image.
- `image_config_entry_point` - (list) - List of values with which to override ENTRYPOINT entry in the image.
- `image_config_working_directory` - (string) - Values with which to override WORKDIR entry in the image.
- `lambda_env` - (map) - Environment parameters passed to the Lambda function
- `lambda_role_policy` (string) - The Lambda IAM Role Policy.
- `log_subscription_filter` - (string) - Subscription filter to filter logs sent to datadog
- `memory_size` (number) - Amount of memory in MB your Lambda Function can use at runtime
- `security_group_ids` - (list) - The VPC security groups assigned to the Lambda.
- `subnet_ids` - (list) - The VPC subnets in which the Lambda runs.
- `timeout` (number) - The maximum time in seconds that the Lambda can run for
- `reserved_concurrent_executions` (number) - The amount of reserved concurrent executions for this lambda function.
- `tags` (map) - A mapping of tags to assign to this lambda function.
- `datadog_log_subscription_arn` - (string) - Log subscription arn for shipping logs to datadog

> NOTE: if both security_group_ids and subnet_ids are empty then the Lambda will not have access to resources within a VPC.

## Usage

```hcl
module "lambda" {
  source        = "github.com/mergermarket/terraform-aws-image-lambda"
  image_uri     = "foo_uri_to_ECR_image"
  function_name = "do_foo"
  timeout       = 5
  memory_size   = 256
  lambda_env    = "${var.lambda_env}"
}
```
Lambda environment variables file:
```json
{
  "lambda_env": {
    "environment_name": "ci-testing"
  }
}
```
