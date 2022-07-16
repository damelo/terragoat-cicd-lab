# My CHECKOV - 3x Fatal ERRORS Found:

## 1º Error: Row 993

Check: CKV_AWS_133: "Ensure that RDS instances has backup policy"
	FAILED for resource: aws_db_instance.default
Error: 	File: /aws/db-app.tf:1-41
	Guide: https://docs.bridgecrew.io/docs/ensure-that-rds-instances-have-backup-policy
		1  | resource "aws_db_instance" "default" {
		2  |   name                   = var.dbname
		3  |   engine                 = "mysql"
		4  |   option_group_name      = aws_db_option_group.default.name
		5  |   parameter_group_name   = aws_db_parameter_group.default.name
		6  |   db_subnet_group_name   = aws_db_subnet_group.default.name
		7  |   vpc_security_group_ids = ["${aws_security_group.default.id}"]
		8  | 
		9  |   identifier              = "rds-${local.resource_prefix.value}"
		10 |   engine_version          = "8.0" # Latest major version 
		11 |   instance_class          = "db.t3.micro"
		12 |   allocated_storage       = "20"
		13 |   username                = "admin"
		14 |   password                = var.password
		15 |   apply_immediately       = true
		16 |   multi_az                = false
		17 |   backup_retention_period = 0
		18 |   storage_encrypted       = false
		19 |   skip_final_snapshot     = true
		20 |   monitoring_interval     = 0
		21 |   publicly_accessible     = true
		22 | 
		23 |   tags = merge({
		24 |     Name        = "${local.resource_prefix.value}-rds"
		25 |     Environment = local.resource_prefix.value
		26 |     }, {
		27 |     git_commit           = "d68d2897add9bc2203a5ed0632a5cdd8ff8cefb0"
		28 |     git_file             = "terraform/aws/db-app.tf"
		29 |     git_last_modified_at = "2020-06-16 14:46:24"
		30 |     git_last_modified_by = "nimrodkor@gmail.com"
		31 |     git_modifiers        = "nimrodkor"
		32 |     git_org              = "bridgecrewio"
		33 |     git_repo             = "terragoat"
		34 |     yor_trace            = "47c13290-c2ce-48a7-b666-1b0085effb92"
		35 |   })
		36 | 
		37 |   # Ignore password changes from tf plan diff
		38 |   lifecycle {
		39 |     ignore_changes = ["password"]
		40 |   }
		41 | }

## 1º ERROR - Solution:

Ensure RDS instances have backup policy

Error: AWS RDS instance without automatic backup setting

Bridgecrew Policy ID: BC_AWS_GENERAL_46
Checkov Check ID: CKV_AWS_133
Severity: MEDIUM

AWS RDS instance without automatic backup setting
Description

This check examines the attribute backup_retention_period this should have a value 1-35, and checks if its set to 0 which would disable the backup.

This check is currently under review and maybe suppressed in future releases.
Fix - Runtime

n/a
Fix - Buildtime
Terraform

    Resource: aws_rds_cluster
    Argument: backup_retention_period

resource "aws_rds_cluster" "test" {
  ...
+ backup_retention_period = 35
}

## 2º Error: Row 1040

Check: CKV_AWS_161: "Ensure RDS database has IAM authentication enabled"
	FAILED for resource: aws_db_instance.default
Error: 	File: /aws/db-app.tf:1-41
	Guide: https://docs.bridgecrew.io/docs/ensure-rds-database-has-iam-authentication-enabled
		1  | resource "aws_db_instance" "default" {
		2  |   name                   = var.dbname
		3  |   engine                 = "mysql"
		4  |   option_group_name      = aws_db_option_group.default.name
		5  |   parameter_group_name   = aws_db_parameter_group.default.name
		6  |   db_subnet_group_name   = aws_db_subnet_group.default.name
		7  |   vpc_security_group_ids = ["${aws_security_group.default.id}"]
		8  | 
		9  |   identifier              = "rds-${local.resource_prefix.value}"
		10 |   engine_version          = "8.0" # Latest major version 
		11 |   instance_class          = "db.t3.micro"
		12 |   allocated_storage       = "20"
		13 |   username                = "admin"
		14 |   password                = var.password
		15 |   apply_immediately       = true
		16 |   multi_az                = false
		17 |   backup_retention_period = 0
		18 |   storage_encrypted       = false
		19 |   skip_final_snapshot     = true
		20 |   monitoring_interval     = 0
		21 |   publicly_accessible     = true
		22 | 
		23 |   tags = merge({
		24 |     Name        = "${local.resource_prefix.value}-rds"
		25 |     Environment = local.resource_prefix.value
		26 |     }, {
		27 |     git_commit           = "d68d2897add9bc2203a5ed0632a5cdd8ff8cefb0"
		28 |     git_file             = "terraform/aws/db-app.tf"
		29 |     git_last_modified_at = "2020-06-16 14:46:24"
		30 |     git_last_modified_by = "nimrodkor@gmail.com"
		31 |     git_modifiers        = "nimrodkor"
		32 |     git_org              = "bridgecrewio"
		33 |     git_repo             = "terragoat"
		34 |     yor_trace            = "47c13290-c2ce-48a7-b666-1b0085effb92"
		35 |   })
		36 | 
		37 |   # Ignore password changes from tf plan diff
		38 |   lifecycle {
		39 |     ignore_changes = ["password"]
		40 |   }
		41 | }

## 2º ERROR - Solution:

Ensure RDS database has IAM authentication enabled

Error: RDS database does not have IAM authentication enabled

Bridgecrew Policy ID: BC_AWS_IAM_65
Checkov Check ID: CKV_AWS_161
Severity: MEDIUM

RDS database does not have IAM authentication enabled
Description

TBD
Fix - Buildtime
Terraform

    Resource: "aws_db_instance
    Argument: iam_database_authentication_enabled

resource "aws_db_instance" "test" {
    ...
+ iam_database_authentication_enabled = true
}

CloudFormation

    Resource: "AWS::RDS::DBInstance
    Argument: Properties.EnableIAMDatabaseAuthentication

Resources:
  DB:
    Type: 'AWS::RDS::DBInstance'
    Properties:
      Engine: 'mysql' # or 'postgres'
      ...
+     EnableIAMDatabaseAuthentication: true

## 3º Error: Row 1087

Check: CKV_AWS_17: "Ensure all data stored in RDS is not publicly accessible"
	FAILED for resource: aws_db_instance.default
Error: 	File: /aws/db-app.tf:1-41
	Guide: https://docs.bridgecrew.io/docs/public_2
		1  | resource "aws_db_instance" "default" {
		2  |   name                   = var.dbname
		3  |   engine                 = "mysql"
		4  |   option_group_name      = aws_db_option_group.default.name
		5  |   parameter_group_name   = aws_db_parameter_group.default.name
		6  |   db_subnet_group_name   = aws_db_subnet_group.default.name
		7  |   vpc_security_group_ids = ["${aws_security_group.default.id}"]
		8  | 
		9  |   identifier              = "rds-${local.resource_prefix.value}"
		10 |   engine_version          = "8.0" # Latest major version 
		11 |   instance_class          = "db.t3.micro"
		12 |   allocated_storage       = "20"
		13 |   username                = "admin"
		14 |   password                = var.password
		15 |   apply_immediately       = true
		16 |   multi_az                = false
		17 |   backup_retention_period = 0
		18 |   storage_encrypted       = false
		19 |   skip_final_snapshot     = true
		20 |   monitoring_interval     = 0
		21 |   publicly_accessible     = true
		22 | 
		23 |   tags = merge({
		24 |     Name        = "${local.resource_prefix.value}-rds"
		25 |     Environment = local.resource_prefix.value
		26 |     }, {
		27 |     git_commit           = "d68d2897add9bc2203a5ed0632a5cdd8ff8cefb0"
		28 |     git_file             = "terraform/aws/db-app.tf"
		29 |     git_last_modified_at = "2020-06-16 14:46:24"
		30 |     git_last_modified_by = "nimrodkor@gmail.com"
		31 |     git_modifiers        = "nimrodkor"
		32 |     git_org              = "bridgecrewio"
		33 |     git_repo             = "terragoat"
		34 |     yor_trace            = "47c13290-c2ce-48a7-b666-1b0085effb92"
		35 |   })
		36 | 
		37 |   # Ignore password changes from tf plan diff
		38 |   lifecycle {
		39 |     ignore_changes = ["password"]
		40 |   }
		41 | }

## 3º ERRO - Solution:

Ensure AWS RDS database instance is not publicly accessible

Error: AWS RDS database instance is publicly accessible

Bridgecrew Policy ID: BC_AWS_PUBLIC_2
Checkov Check ID: CKV_AWS_17
Severity: HIGH

AWS RDS database instance is publicly accessible
Description

Ensure that all your public AWS Application Load Balancer are integrated with the Web Application Firewall (AWS WAF) service to protect against application-layer attacks. An Application Load Balancer functions at the application layer, the seventh layer of the Open Systems Interconnection (OSI) model. After the load balancer receives a request, it evaluates the listener rules in priority order to determine which rule to apply, and then selects a target from the target group for the rule action. You can configure listener rules to route requests to different target groups based on the content of the application traffic. Routing is performed independently for each target group, even when a target is registered with multiple target groups.
Fix - Runtime
AWS Console

To change the policy using the AWS Console, follow these steps:

    Log in to the AWS Management Console at https://console.aws.amazon.com/.
    Open the Amazon RDS console.
    On the navigation pane, click Snapshots.
    Select the snapshot to encrypt.
    Navigate to Snapshot Actions, select Copy Snapshot.
    Select your Destination Region, then enter your New DB Snapshot Identifier.
    Set Enable Encryption to Yes.
    Select your Master Key from the list, then select Copy Snapshot.

Fix - Buildtime
Terraform

    Resource: aws_db_instance
    Argument: publicly_accessible

resource "aws_db_instance" "default" {
  ...
+ publicly_accessible   = false
}

CloudFormation

    Resource: AWS::RDS::DBInstance
    Argument: Properties.PubliclyAccessible

Type: 'AWS::RDS::DBInstance'
    Properties:
      ...
+     PubliclyAccessible: false