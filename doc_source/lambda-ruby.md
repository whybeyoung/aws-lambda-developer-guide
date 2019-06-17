# Building Lambda Functions with Ruby<a name="lambda-ruby"></a>

You can run Ruby code in AWS Lambda\. Lambda provides [runtimes](lambda-runtimes.md) for Ruby that execute your code to process events\. Your code runs in an environment that includes the AWS SDK for Ruby, with credentials from an AWS Identity and Access Management \(IAM\) role that you manage\.

Lambda supports the following Ruby runtimes\.


**Ruby Runtimes**  

| Name | Identifier | AWS SDK for Ruby | Operating System | 
| --- | --- | --- | --- | 
|  Ruby 2\.5  |  `ruby2.5`  |  3\.0\.1  |  Amazon Linux  | 

Lambda functions use an [execution role](lambda-intro-execution-role.md) to get permission to write logs to Amazon CloudWatch Logs and access other services and resources\. If you don't already have an execution role for function development, create one\.

**To create an execution role**

1. Open the [roles page](https://console.aws.amazon.com/iam/home#/roles) in the IAM console\.

1. Choose **Create role**\.

1. Create a role with the following properties\.
   + **Trusted entity** – **Lambda**\.
   + **Permissions** – **AWSLambdaBasicExecutionRole**\.
   + **Role name** – **lambda\-role**\.

   The **AWSLambdaBasicExecutionRole** policy has the permissions that the function needs to write logs to CloudWatch Logs\.

You can add permissions to the role later, or swap it out for a different role that's specific to a single function\.

**To create a Ruby function**

1. Open the [Lambda console](https://console.aws.amazon.com/lambda)\.

1. Choose **Create function**\.

1. Configure the following settings:
   + **Name** – **my\-function**\.
   + **Runtime** – **Ruby 2\.5**\.
   + **Role** – **Choose an existing role**\.
   + **Existing role** – **lambda\-role**\.

1. Choose **Create function**\.

1. To configure a test event, choose **Test**\.

1. For **Event name**, enter **test**\.

1. Choose **Create**\.

1. To execute the function, choose **Test**\.

The console creates a Lambda function with a single source file named `lambda_function.rb`\. You can edit this file and add more files in the built\-in [code editor](code-editor.md)\. Choose **Save** to save your changes, and choose **Test** to run your code\.

**Note**  
The Lambda console uses AWS Cloud9 to provide an integrated development environment in the browser\. You can also use AWS Cloud9 to develop Lambda functions in your own environment\. See [Working with AWS Lambda Functions](https://docs.aws.amazon.com/cloud9/latest/user-guide/lambda-functions.html) in the AWS Cloud9 user guide for more information\.

`lambda_function.rb` exports a function named `lambda_handler` that takes an event object and a context object\. This is the [handler function](ruby-handler.md) that Lambda calls when the function is invoked\. The Ruby function runtime gets invocation events from Lambda and passes them to the handler\.

Each time you save your function code, the Lambda console creates a deployment package, which is a ZIP archive that contains your function code\. As your function development progresses, you will want to store your function code in source control, add libraries, and automate deployments\. Start by [creating a deployment package](ruby-package.md) and updating your code at the command line\.

The function runtime passes a context object to the handler, in addition to the invocation event\. The [context object](ruby-context.md) contains additional information about the invocation, the function, and the execution environment\. Further information is available from environment variables\.

Your Lambda function comes with a CloudWatch Logs log group\. The function runtime sends details about each invocation to CloudWatch Logs, and relays any [logs that your function outputs](ruby-logging.md) during invocation\. If your function [returns an error](ruby-exceptions.md), Lambda formats the error and returns it to the invoker\.

**Topics**
+ [AWS Lambda Function Handler in Ruby](ruby-handler.md)
+ [AWS Lambda Deployment Package in Ruby](ruby-package.md)
+ [AWS Lambda Context Object in Ruby](ruby-context.md)
+ [AWS Lambda Function Logging in Ruby](ruby-logging.md)
+ [AWS Lambda Function Errors in Ruby](ruby-exceptions.md)