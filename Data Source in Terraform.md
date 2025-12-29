Data Source in Terraform 

What
A data source is used to read existing information from AWS (or other providers).
It does not create anything. It only fetches data.

Why
We use a data source when the resource is already created and we just want to use its details (ID, IP, ARN, etc.) in our Terraform code.

How (Example)
Example: An EC2 instance already exists. You want its ID.

data "aws_instance" "my_ec2" {
  instance_id = "i-0abc12345xyz"
}

output "ec2_id" {
  value = data.aws_instance.my_ec2.id
}


Explanation

data "aws_instance" → tells Terraform to read an existing EC2

instance_id → which EC2 to read

data.aws_instance.my_ec2.id → use the fetched value

Another Common Example (AMI)

data "aws_ami" "amazon_linux" {
  most_recent = true
  owners      = ["amazon"]

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*"]
  }
}


Used later like this:

ami = data.aws_ami.amazon_linux.id


In one line
👉 Resource = create
👉 Data source = read existing


////////////////////

data "aws_ami" "amazon_linux" {
  most_recent = true

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*"]
  }

  owners = ["amazon"]
}

Why both are used together (important)

If you use only filter ❌
→ Terraform may pick an old AMI

If you use only most_recent ❌
→ Terraform may pick the latest wrong AMI

✅ Filter + most_recent
→ Latest correct AMI
