# S3 Presigned URLs Task

## Objective

Learn how to generate presigned URLs for Amazon S3 objects to securely share them or grant temporary access without altering your bucket's permissions. This task involves creating an S3 bucket, uploading an object, and generating a presigned URL to access the object.

## Prerequisites

-   AWS CLI installed and configured on your machine.
-   Basic understanding of AWS S3 and permissions.

## Task Overview

You will create an S3 bucket, upload a sample object, and then generate a presigned URL to provide temporary access to the object. Finally, you will test the presigned URL to ensure it grants access as expected.

### Step 1: Create an S3 Bucket

1.  Open your terminal.
    
2.  Run the following command to create a new S3 bucket. Replace `your-unique-bucket-name` with a unique name for your bucket:
    
    `aws s3 mb s3://your-unique-bucket-name` 
    

### Step 2: Upload a Sample Object

1.  Create a simple text file named `sample.txt` with some content.
    
2.  Upload the file to your newly created bucket:
   
    
    `aws s3 cp sample.txt s3://your-unique-bucket-name/sample.txt` 
    

### Step 3: Generate a Presigned URL

1.  Use the AWS CLI to generate a presigned URL for the `sample.txt` object. Replace `your-unique-bucket-name` with your bucket's name and specify an expiration time in seconds:
    
    `aws s3 presign s3://your-unique-bucket-name/sample.txt --expires-in 3600` 
    
    This command will generate a presigned URL that grants temporary access to the `sample.txt` object for 1 hour (3600 seconds).
    

### Step 4: Test the Presigned URL

1.  Copy the presigned URL generated in the previous step.
    
2.  Paste the URL into a web browser or use `curl` to access the object:
    
    `curl "PRESIGNED_URL"` 
    
    Replace `PRESIGNED_URL` with the actual presigned URL. You should be able to access the content of `sample.txt` without any access denied errors.
    

## Deliverables

-   The S3 bucket name and the name of the uploaded object.
-   The command used to generate the presigned URL and the actual presigned URL.
-   Confirmation that the presigned URL was successfully tested and the content of `sample.txt` was accessible.

## Evaluation Criteria

-   Successful creation of an S3 bucket and upload of an object.
-   Correct generation of a presigned URL with an appropriate expiration time.
-   Successful access to the S3 object using the presigned URL, demonstrating understanding of S3 presigned URLs and their temporary nature.
