Terraform State Lock (DynamoDB) – Simple Explanation

What
Terraform state lock prevents more than one Terraform run from changing the same state file at the same time.
The DynamoDB table is used to store this lock information.

Why

To avoid state file corruption
To stop two users / pipelines from running terraform apply at the same time
Very important for team work and CI/CD
Without lock → state file can break ❌
With lock → safe changes ✅

How

When you run terraform apply:
Terraform creates a lock entry in DynamoDB
Other users cannot run apply until it finishes
After apply completes:
Lock is released automatically
If someone else tries:
Error: state is locked
