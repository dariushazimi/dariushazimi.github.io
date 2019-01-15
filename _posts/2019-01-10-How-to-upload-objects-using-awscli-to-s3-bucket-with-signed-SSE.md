# How to upload objects using AWS CLI to S3 bucket with assigned SSE?

Keep in mind Server-side encryption is about protecting data at rest.
In short here is the command to upload objects using AWS CLI to S3 bucket with assigned SSE.

`aws s3 cp <local path> <s3 path> --sse AES256i`

## S3 Server side encryption
When S3 receives your object, it calls KMS to create a data key, encrypts your data with that data key (not the master key), and stores the encrypted data key along with the encrypted data.
When you try to download the encrypted files, S3 sees it has been encrypted, asks KMS to decrypt the data key (using the master key), and then uses the decrypted data key to decrypt the data before returning to you. My understanding from the docs and from the way SSE and KMS work is that there is no assumption on the user needing to have access to the master key for that to work -- it suffices that S3 has access to it.
## S3 client-side encryption
Client-side encryption refers to encrypting data before sending it to Amazon S3.
In this scenario, the S3 client (instead of S3 on the backend) will ask for a KMS data key (derived from the master key), encrypt data client-side and upload it. It will not be possible to decrypt it on the server, and when clients download the (encrypted) files, decryption needs to happen client-side (the S3 client deals with that for you, though).
