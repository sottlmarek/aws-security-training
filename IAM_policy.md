## AWS IAM Policy Document Training Task

### Objective

Create a custom IAM policy that grants specific permissions to an S3 bucket named `training-bucket`. The policy should allow listing, reading, and writing objects but should not permit object deletion.

### Instructions

#### Step 1: Define the Policy Document

Start by defining your policy document in JSON format. This policy allows actions like `s3:ListBucket`, `s3:GetObject`, and `s3:PutObject` on the specified bucket and its contents, without granting delete permissions.

    `{
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "s3:ListBucket",
                    "s3:GetObject",
                    "s3:PutObject"
                ],
                "Resource": [
                    "arn:aws:s3:::training-bucket",
                    "arn:aws:s3:::training-bucket/*"
                ]
            }
        ]
    }` 

#### Step 2: Create the Policy in AWS

Use the AWS Management Console or the AWS CLI to create the policy with the JSON document you've defined.

##### Using AWS Management Console:

1.  Navigate to the IAM dashboard.
2.  Select "Policies" from the sidebar and click "Create policy".
3.  Switch to the JSON tab and paste your policy document.
4.  Click "Review policy", give it a name like `S3_TrainingBucketAccessPolicy`, and create the policy.

##### Using AWS CLI:

If you prefer using the AWS CLI, save your policy document as `s3_policy.json` and execute the following command:


`aws iam create-policy --policy-name S3_TrainingBucketAccessPolicy --policy-document file://s3_policy.json` 

#### Step 3: Attach the Policy to a User or Role

After creating the policy, attach it to an IAM user or role that requires these permissions.

##### Using AWS Management Console:

1.  Navigate to the IAM dashboard.
2.  Select "Users" or "Roles" from the sidebar.
3.  Choose the user or role to attach the policy to.
4.  Under the "Permissions" tab, click "Add permissions".
5.  Choose "Attach existing policies directly" and select the policy you created.
6.  Click "Next: Review" and then "Add permissions".

##### Using AWS CLI:

To attach the policy to a user, use the following command, replacing `Jim` with the actual user's name:


`aws iam attach-user-policy --user-name Jim --policy-arn arn:aws:iam::aws:policy/S3_TrainingBucketAccessPolicy` 

To attach it to a role, replace `RoleName` with the actual role's name:


`aws iam attach-role-policy --role-name RoleName --policy-arn arn:aws:iam::aws:policy/S3_TrainingBucketAccessPolicy` 

### Deliverables

-   Screenshot of the policy JSON document in the AWS Management Console or the output of the AWS CLI command that created the policy.
-   Explanation of the policy's purpose and its restrictions, focusing on why it does not permit object deletion.

### Evaluation Criteria

-   The policy correctly grants the specified permissions without allowing object deletion.
-   The policy is successfully attached to an IAM user or role, demonstrating its application in a real-world scenario.
