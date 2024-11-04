# Task: Export SBOM Using Amazon Inspector

## Objective
Learn to export a Software Bill of Materials (SBOM) for AWS resources using Amazon Inspector and securely store the report using S3 and KMS encryption.

## Prerequisites
- AWS account with access to Amazon Inspector, S3, and KMS.
- Appropriate permissions to create and manage Inspector assessments, S3 buckets, and KMS keys.

## Task Steps

### Step 1: Set Up AWS Resources
1. **Create a KMS Encryption Key**:
    - Use the AWS CLI to create a new KMS key specifically for encrypting the SBOM stored in S3.
    ```bash
    aws kms create-key --description "Encryption key for SBOM bucket"
    ```
    - Capture the `KeyId` from the output to use in the S3 bucket encryption configuration and KMS key policy.
    - Enter this the AWS KMS key ARN configured for Amazon Inspector to use for encrypting the SBOM reports.
    - Ensure the KMS key policy is set as follows:
        ```json
        {
            "Version": "2012-10-17",
            "Id": "key-sbom",
            "Statement": [
                {
                    "Sid": "Allow Inspector to use the key",
                    "Effect": "Allow",
                    "Principal": {"Service": "inspector2.amazonaws.com"},
                    "Action": ["kms:Decrypt", "kms:GenerateDataKey*", "kms:Encrypt"],
                    "Resource": "*",
                    "Condition": {
                        "StringEquals": {"aws:SourceAccount": "[ACCOUNT-ID]"},
                        "ArnLike": {"aws:SourceArn": "arn:aws:inspector2:[REGION]:[ACCOUNT-ID]:report/*"}
                    }
                }
            ]
        }
        ```

2. **Create an S3 Bucket**:
    - Create an S3 bucket to store the exported SBOM.
    - Enable encryption on the bucket using the KMS key created in the previous step.
    - Configure the bucket policy to allow Amazon Inspector to put objects.
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Sid": "allow-inspector",
                "Effect": "Allow",
                "Principal": {"Service": "inspector2.amazonaws.com"},
                "Action": ["s3:PutObject", "s3:PutObjectAcl", "s3:AbortMultipartUpload"],
                "Resource": "arn:aws:s3:::your-sbom-bucket/*",
                "Condition": {
                    "StringEquals": {"aws:SourceAccount": "[ACCOUNT-ID]"},
                    "ArnLike": {"aws:SourceArn": "arn:aws:inspector2:[REGION]:[ACCOUNT-ID]:report/*"}
                }
            }
        ]
    }
    ```

### Step 2: Access Amazon Inspector
1. Navigate to the [Amazon Inspector console](https://console.aws.amazon.com/inspector/v2/home).

### Step 3: Select AWS Region
1. **Choose the Region** that contains the resources for which you want to export an SBOM using the AWS Region selector in the upper-right corner of the Amazon Inspector console.

### Step 4: Initiate SBOM Export
1. **Navigate to Export Option** in the navigation pane and click on **Export SBOMs**.
2. **Apply Filters** (Optional) to select specific resources for the SBOM report.

### Step 5: Configure Export Settings
1. **Select the SBOM Format** (e.g., CycloneDX, SPDX).
2. **Specify the S3 Storage Location** by entering the URI of the bucket created in Step 1.

### Step 6: Export SBOM
1. **Start the Export** process by confirming all settings and initiating the export of the SBOM.

## Deliverables
- A screenshot or log of the SBOM export confirmation page.
- A link to the S3 bucket containing the exported SBOM.
- Documentation of the KMS key used for encryption.

## Evaluation Criteria
- Successful export of the SBOM to the specified S3 location.
- Proper encryption of the SBOM using the specified AWS KMS key.
- Correct application of optional resource filters if used.

By completing this task, participants will gain hands-on experience in using AWS services to enhance security and compliance through the generation and secure storage of SBOMs.
