terraform validate

What
terraform validate checks whether your Terraform configuration is syntactically correct.

Why
We use it to make sure there are no errors in the configuration before running plan or apply.

Where
Used after writing Terraform code and before terraform plan.

How
Run this command:

terraform validate

Example

If you forget required value like ami in EC2 resource, it will show an error.
