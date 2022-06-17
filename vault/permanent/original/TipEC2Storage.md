# TipEC2Storage

By itself, [[EC2]] offers only the Instance Storage. These are #temporary [[Block Storage]] that are saved on #disks, directly attached to the [[instances]]. They are the *#fastest storage* offering, but offer very *little #durability*, being available only during the lifetime of instances - Saved between restarts but lost on Stop and Terminations.

The usual solution is to use attached [[EBS]] volumes or [[EFS]] in the case of Block Level #Storage, and [[S3]] #buckets for object storage.