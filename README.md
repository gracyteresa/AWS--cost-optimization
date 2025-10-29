**AWS Cost Optimization Using Lambda and CloudWatch for Stale Resource Cleanup**
In this project, I designed and implemented an automated AWS cost optimization process that identifies and deletes stale EBS snapshots to reduce unnecessary storage costs.

##Problem Overview
In AWS, when an EC2 instance is created, a volume (EBS) is typically attached to it. Many users create EBS snapshots of these volumes for backup or recovery purposes. However, after instances or volumes are deleted, their associated snapshots often remain unused. These orphaned or stale snapshots continue to incur storage charges, contributing to increased operational costs over time.

##Solution Overview
To address this, I developed an automated cleanup solution using:
• AWS Lambda (serverless function)
•	Amazon CloudWatch EventBridge (for scheduling)
•	Boto3 SDK (for AWS API interactions)

**##Working Mechanism**
1.	Scheduled Trigger using CloudWatch:
o	A CloudWatch EventBridge rule is configured to trigger the Lambda function at a scheduled interval (for example, once every day or week).
o	This ensures continuous monitoring of stale snapshots without manual intervention.

2. Lambda Function Logic:
o	The Lambda function uses Boto3 (Python SDK for AWS) to interact with EC2 and EBS services.
o	It fetches all available EBS snapshots in the account.

For each snapshot:
It checks whether the associated volume ID exists.
If the volume is missing (indicating it was deleted), the snapshot is considered stale.
It further checks if the volume’s instance still exists; if not, it’s also treated as unattached and unnecessary.	If a snapshot meets these stale conditions, it is automatically deleted using the EC2 delete_snapshot() API call.

##Cost Optimization:
	By automatically removing snapshots not linked to any active volume or instance, the system ensures that only necessary snapshots remain.
  This results in reduced storage costs and optimized resource utilization.
  
##Benefits
•	Automated and scheduled cleanup without manual monitoring.
•	Reduces AWS costs by deleting unused EBS snapshots.
•	Enhances cloud hygiene, ensuring the environment remains clean and efficient.
•	Scalable and can be extended to handle other unused resources (like unattached volumes or idle Elastic IPs).

##Tech Stack
•	AWS Lambda (Python 3.x)
•	Boto3 (AWS SDK for Python)
•	Amazon CloudWatch EventBridge (for scheduling)
•	IAM Role (with permissions for EC2:DescribeSnapshots, EC2:DescribeVolumes, and EC2:DeleteSnapshot)
<img width="578" height="253" alt="image" src="https://github.com/user-attachments/assets/da433d42-ced1-41e2-941f-8d591d99dfdf" />


