# terraform-beta EMR
For release terraform EMR beta binary

## Sample specs. for testing

- emr-cluster.tf

```
resource "aws_emr" "tf-test-cluster" {
  name          = "tf-emr-cluster"
  release_label = "emr-4.6.0"
  applications  = ["Spark"]

  ec2_attributes {
    key_name                          = "xxxx_key"
    subnet_id                         = "subnet-xxxx"
    additional_master_security_groups = "sg-xxxx"
  }

  use_default_roles = true
  log_uri           = "s3://testbucket/emr-spark-test/"

  master_instance_type = "m3.xlarge"
  core_instance_type   = "m3.xlarge"
  core_instance_count  = 1 

}
```

- emr-task.tf
```
resource "aws_emr_task_group" "task1" {
  cluster_id     = "${aws_emr.tf-test-cluster.id}"
  instance_count = 2 
  instance_type  = "m3.xlarge"
}
```
