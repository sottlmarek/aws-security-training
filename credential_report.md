# AWS IAM Credential Report Task

## Objective

Learn how to generate and analyze an IAM credential report in AWS to enhance your account's security posture. This task involves generating a credential report, retrieving it, decoding it, and identifying potential security concerns based on the report's contents.

## Prerequisites

-   Basic knowledge of AWS IAM
-   AWS CLI installed and configured with appropriate permissions

## Task Steps

### 1. Generate IAM Credential Report

Start by generating a new IAM credential report. This report will contain details about each IAM user's status within your AWS account.


`aws iam generate-credential-report` 

You should see a response indicating that the report generation has started or is complete.

### 2. Retrieve the Credential Report

Once the report generation is complete, retrieve the generated IAM credential report using the following command:


`aws iam get-credential-report` 

This will return a JSON object, including the credential report in a base64-encoded format.

### 3. Decode the Credential Report

To decode and view the content of the credential report in a human-readable format, use the following command:


`aws iam get-credential-report --output text --query Content | base64 --decode` 

### 4. Analyze the Report

Review the decoded credential report and focus on the following columns to identify potential security concerns:

-   `user`
-   `password_enabled`
-   `password_last_used`
-   `password_last_changed`

Look for any IAM users with passwords that have not been changed in an extended period, which could indicate a lapse in security practices.

### 5. Summarize Your Findings

Based on your analysis, summarize any security concerns you've identified. Highlight users with outdated password practices or any other potential security risks.

## Deliverables

-   A written summary of your findings, detailing any security concerns and suggested actions to mitigate these risks.

## Evaluation Criteria

-   Successful execution of commands to generate, retrieve, and decode the IAM credential report.
-   Thorough analysis of the credential report, identifying potential security concerns.
-   Clear and actionable recommendations in the summary to improve the security posture based on the findings.
