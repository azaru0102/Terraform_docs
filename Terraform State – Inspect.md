terraform state list  -- Shows all resources stored inside the Terraform state file. To check what Terraform is currently managing we used this command.

terraform state show -- Displays detailed information about a specific resource in state. To see current configuration values stored in state. Used when troubleshooting or verifying attributes 
 ( terraform state show aws_instance.myserver ) 


 terraform graph -- Shows dependency graph of resources. To understand resource dependency flow. Used during debugging complex infrastructure. 
 terraform output -- Displays output values defined in outputs.tf  To get important values like public IP, DNS name. 

 terraform state rm -- Removes a resource from state (does NOT delete real resource).  To stop Terraform from managing a resource. When resource exists but you don't want Terraform control.
 example :   terraform state rm aws_instance.myserver

 terraform state mv -- Moves a resource from one name to another inside state. Used during refactoring (rename resource block). When changing resource names in code. 
 example : terraform state mv aws_instance.old aws_instance.new 

 -replace option in apply -- Forces Terraform to destroy and recreate a resource. When resource is corrupted or needs full rebuild. During apply command.
 example: terraform apply -replace="aws_instance.myserver"

 terraform state pull / push -- Pull = Download state file  / Push = Upload state file. Used in remote backend troubleshooting.
 Example
 You want to manually inspect S3 state file.


terraform state replace-provider --  is used to change the provider reference inside the Terraform state file.
It does NOT recreate resources.
It only updates which provider manages them. 
When you change the provider source (example: public registry → private company registry), Terraform must know that existing resources now belong to the new provider.

example : terraform state replace-provider OLD_PROVIDER NEW_PROVIDER

terraform force-unlock is used to manually remove a Terraform state lock.

It unlocks the state file when it is stuck. Terraform locks the state to prevent multiple people from running apply at the same time.

If a previous apply fails or is interrupted, the lock may remain.
 
