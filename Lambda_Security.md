# AWS Lambda Task: List Objects in an S3 Bucket

## Objective

Create an AWS Lambda function that lists objects in an S3 bucket named `supercoolbucket`. This task will help you understand how to interact with S3 using Lambda and `boto3`, and how to configure the necessary permissions for a Lambda function.

## Prerequisites

-   Basic understanding of AWS Lambda, S3, and IAM roles.
-   AWS account with access to Lambda, S3, and IAM.

## Task Description

You are to write a Lambda function in Python using the `boto3` library. The function should list all objects in the S3 bucket named `supercoolbucket`. You'll also create an IAM role that grants your Lambda function access to read from S3.

### Step 1: Prepare the IAM Role

1.  **Create a new IAM role** in the AWS Management Console under the IAM service.
2.  **Attach the AWS managed policy** `AmazonS3ReadOnlyAccess` to this role. This policy grants the necessary permissions to list objects in an S3 bucket.

### Step 2: Write the Lambda Function

Use the following Python code for your Lambda function. This code utilizes `boto3` to list objects in the specified S3 bucket.

`import boto3

def lambda_handler(event, context):
    # Initialize a boto3 client
    s3 = boto3.client('s3')

    # Name of the S3 bucket
    bucket_name = 'supercoolbucket'

    # List objects within the bucket
    response = s3.list_objects_v2(Bucket=bucket_name)

    # Extract the list of object summaries
    objects = response.get('Contents', [])

    # Print object names
    for obj in objects:
        print(f"Object: {obj['Key']}")

    return {
        'statusCode': 200,
        'body': f"Listed {len(objects)} objects from {bucket_name}"
    }` 

### Step 3: Deploy the Lambda Function

1.  **Navigate to the AWS Lambda service** in the AWS Management Console.
2.  **Create a new Lambda function** and select the Python runtime.
3.  **Paste the provided Python code** into the online code editor.
4.  **Assign the previously created IAM role** to this Lambda function.
5.  **Deploy the Lambda function.**

### Step 4: Test Your Lambda Function

1.  **Create a test event** in the Lambda console. The event details do not matter for this function, as it does not use event data.
2.  **Invoke the Lambda function** using the test event and verify that it lists the contents of `supercoolbucket`.

## Deliverables

-   The Python code for the Lambda function.
-   A screenshot of the Lambda function configuration, showing the assigned IAM role.
-   Output logs from a test invocation of the Lambda function, demonstrating successful listing of objects in the bucket.

## Evaluation Criteria

-   Successful execution of the Lambda function, demonstrating the ability to list objects in the specified S3 bucket.
-   Correct assignment of IAM role with minimal necessary permissions (`AmazonS3ReadOnlyAccess`).
-   Proper handling and logging of the listed objects and potential errors.
