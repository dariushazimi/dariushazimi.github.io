# Resizing EC2 with boto3

Th script is using boto3 to stop an EC2 instance, resize the instance, then start the instance back up. 

> *Copyright 2018 [Dariush Azimi](http://dariushazimi.com)*

## Prerequisites

- You need to have Boto3 installed.



```
import boto3

client = boto3.client('ec2')

# Insert your Instance ID here
my_instance = 'i-xxxxxxxx'

# Stop the instance
client.stop_instances(InstanceIds=[my_instance])
waiter=client.get_waiter('instance_stopped')
waiter.wait(InstanceIds=[my_instance])

# Change the instance type
client.modify_instance_attribute(InstanceId=my_instance, Attribute='instanceType', Value='m3.xlarge')

# Start the instance
client.start_instances(InstanceIds=[my_instance])
```

