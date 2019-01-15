# What you need to know about Cross Region Replication (CRR)?
When you create an s3 bucket and trun on replication, it replicates from one region to another, by default this is done using SSL. 
So there is no need to turn this on or set a policy.

-	You can only replicate from the source bucket to only ONE another bucket. (its not like read replicas in RDS)
-	It is a one to one replationship
-	Source and desitnation must have versioning turned on
-	Source and destination must be in different regions
-	If the source owner of the bucket owns the objects inside the bucket, the owner has full permission otherwise you must use ACL to grand read and write permission
-	Replication works accros accounts
-	The IAM role must have permission to replicate to the destination bucket
-	If you turn on cloud trail, and then replicate the logs from the S3 to another s3 region (do this) to secure the cloud trial logs, have a sepreate aws account to replicate to another account. 
-	Only objects created after the replication is turned on, will be replicated
-	Ensure that you have access to read the source objects.
-	If you delete an object from the source s3, essentially you are placing a delete marker and this marker is also replicated
## What is not replicated?
- Anything before Cros region replicatioin was turned on
- Objects crated with server side encryption using custom managed keys SSE-C
- SSE-KMS must be explicity enabled
- Deletes of a particular version of an object 
  - Delete marker is actually hiding the file, to restore the file, you just remove the delte marker

- Remember for CRR, you don’t need to turn on the bucket policy for secure transport, that is done by default
- Delete markers are replicated but deleted version of the objects not.
- Versining must be enabled
- It is poissible to use CRR between mutople aws accounts, IAM role must have access to the destination bucket.to use CRR between mutople aws accounts, IAM role must have access to the destination bucket.
- Enable CRR for cloud trails logs for replicate to another bucket in another account where only the auditors have access to.
