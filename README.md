# terraform-beta 
------------------

@This one deprecated, all the code was merged with Terraform main release,
Please refer to the official binary and docs.


## Download
* Mac OSX
https://github.com/IAops/terraform-beta/raw/master/darwin_amd64.zip

* Linux
https://github.com/IAops/terraform-beta/raw/master/linux_amd64.zip

## EMR features
- Master, Core cluster create, resize, destroy
- Task instance groups create, resize
- Two resource types: aws_emr, aws_emr_task_group


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
