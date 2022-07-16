# CHECKOV - Fatal ERROS

## 1° Error: Row 993

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

## 2° Error: Row 1040

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

## 3° Error: Row 1087

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
