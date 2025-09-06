# osas_python_ec2_status_check

## Background Info

 Assuming you have autoscaling configured and you have hundreds of instances, what if you want to know which instances are in which state? i.e are they initializing? Stopped? Running?
If we want live status updates, we can’t keep running the program manually, so we need some automated process that triggers the program automatically. This is one of the advantages of python programs: we can use python as scheduled tasks

## Project Description

In this project, we will use python to  create an automated scheduled task in python that gives you state of instances. We will write a scheduler that will execute the above logic every 5 minutes.


## Requirements

- Python 3.7+
- AWS credentials configured 
- EC2 instance running
- Installed Python packages: boto3, schedule

## Configure your AWS credentials
Execute the command below and follow the prompts

```
aws configure
```

## Add scheduler library to the project
```
pip install schedule

```
  and then import schedule



# Create EC2 instances with TF: 

I already had instances created using terraform. The region in the terraform provide must match the region in the referenced boto3 library.

# Create a function 

Using boto3, fetch all the instances running in this region. How do we get info from instances regardless of which instances they’re running? ***Ec2_client.describe_instances()***
and then saving it into a variable ("statuses"), and printing it. This execution will return reservations. 
Reservations is the start/launching of instances; each reservation can have multiple instances. The state is nested in the instance, which is nested in the reservations. We need to access the state. We can do this using ***for loops***

## Things to consider

Note that “describe_instance_status" only shows instances in the running state, and not terminated instances. If we want to  display terminated instances as well, we will use the attribute ***IncludeAllInstances=True*** in the statuses in the function. 


# Run scheduled tasks continuously
Run the script in an infinite loop using:
```
while True:
    schedule.run_pending()

```
