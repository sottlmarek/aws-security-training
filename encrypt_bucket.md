# Encryption Practice Task: Securing S3 Buckets with AWS KMS

## Objective

Enhance data security by implementing encryption on an Amazon S3 bucket using AWS Key Management Service (KMS). This task involves encrypting an existing S3 bucket and ensuring all new objects are encrypted by default.

## Prerequisites

-   Basic knowledge of Amazon S3 and AWS KMS.
-   AWS CLI installed and configured, or access to the AWS Management Console.

## Task Description

You are tasked with securing sensitive data stored in an Amazon S3 bucket named `sensitive-data-bucket`. To achieve this, you'll utilize AWS Key Management Service (KMS) to encrypt the data. The task is divided into two main parts: encrypting existing objects and setting up default encryption for new objects.

### Part 1: Encrypt Existing Objects in S3 Bucket

1.  **Create a KMS Key:**
    
    -   Via AWS Management Console:
        -   Navigate to the KMS section, choose "Create a key", and follow the prompts.
    -   Via AWS CLI:
        -   Run `aws kms create-key --description "S3 bucket encryption key"`.
2.  **Encrypt Existing S3 Objects:**
    
    -   Write a script or use AWS CLI to copy the existing objects in the bucket to themselves while applying SSE-KMS encryption. Use the KMS key created in the previous step.
    -   Example AWS CLI command:
        
        `aws s3 cp s3://sensitive-data-bucket/<object-key> s3://sensitive-data-bucket/<object-key> --sse aws:kms --sse-kms-key-id <KMSKeyId>` 
        
    -   Replace `<object-key>` with the actual key of the object and `<KMSKeyId>` with the ID of your KMS key.

### Part 2: Enable Default Encryption for New Objects

1.  **Set Default Bucket Encryption:**
    -   Via AWS Management Console:
        -   Navigate to the S3 bucket properties, find the "Default encryption" setting, and choose to encrypt with AWS KMS. Select the KMS key you created.
    -   Via AWS CLI:
        -   Run `aws s3api put-bucket-encryption --bucket sensitive-data-bucket --server-side-encryption-configuration '{"Rules":[{"ApplyServerSideEncryptionByDefault":{"SSEAlgorithm":"aws:kms","KMSMasterKeyID":"<KMSKeyId>"}}]}'`.
    -   Replace `<KMSKeyId>` with the ID of your KMS key.
