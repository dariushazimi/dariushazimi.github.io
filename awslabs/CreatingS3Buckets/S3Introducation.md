## Introducing S3 Bucket
S3 is object based stroage, meaning you can store files and folders but not operating systems or database.
1. Files can be upto 5TB
2. Unlimited storage
3. Files are stored in buckets
4. S3 is a universal name space and must be unique globally
   ` https://s3-eu-west-1.amazonaws.com/01winter20180908`
5. Read after write conistency for puts of new objects
6. Eventual consistency for overwrite PUTS and Deletes (takes time to propogate) - [click here for more info](https://aws.amazon.com/s3/storage-classes/)
7. Built for 99.99% availability
8. Guarantees 99.999999999% (11 9s) durability for s3 (pretty much 100% durable)
9. Lifecycle mgm, based on the age of the file
10. Versioning
11. Encruption
## Creating S3 buckets
1. Create a bucket (use a uniqe name)
2. Enable versioning (once enabled can only be suspended, can't disable versioning)
3. Under managemnet, create a rule for lifecycle, `s3lifecycle01`
4. Enable current version and previous version set 30/60 days respectivly
5. Notice it defaults to 425 days.  it's defaulting to a year (365 days) after your last lifecycle movement. 365 days after your objects transition to Glacier, which, in turn, happen 60 days from object creation.

 :warning: 
 - Lifecycle can be used in conjuction with versioning
 - can be applied to current and pervious versions
 - by default, new created buckets are private
 - you can setup access control to your buckets using both:
    -  bucket policies
    -  access control list (can drill down to individual objects)
- S3 buckets can log access request to another bucket or even another account
- Snowball
Petabyte-scale data transport solutionthat suses secure appliances to transfer large amount of data into and out of AWS.

![image](https://dhenschen.files.wordpress.com/2015/10/aws-snowball.jpg)
- 