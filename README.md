# Code Deploy Class

Code for the class <https://udemy.com/course/aws-codedeploy>. The class is a bit out of date, so this
repository updates the creation of the items

## Cloudformation

run in the following order:

* codedeploy-iam.yaml
* codedeploy-vpc.yaml
* codedeploy-infra-linux.yaml


## Github Repository Contains The Deployable Bundle

<https://github.com/donhenton/github-codedeploy>. Is the item that gets deployed in the video

## Attic

The attic entries include the full item from the class (codedeploy-infra) and an attempt to use
imports from vpc

## Docker Compose

Creates a single EC2 instance with Docker and Docker Compose in user data.

## Code Deploy

* create an EC2/On Premises application with a  Deployment group that contains a service role and a deployment type
* service role should have AWSCodeDeployRole attached
* deployment type is all at once or red green

## IAM Permissions For EC2 Instances

InstanceProfile Policy -- attached to EC2 Service Role --> attached to EC2 instances via cloudformation
codedeploy-infra-linux.yml (InstanceProfile parameter).

You can find the ARN by going to the EC2 role, and find it there, the only way to create this ARN is with an EC2 service role

### Profile Policy

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "s3:Get*",
                "s3:List*"
            ],
            "Resource": [
                "arn:aws:s3:::com.awsdhenton.deploy-bucket",
                "arn:aws:s3:::com.awsdhenton.deploy-bucket/*"
            ]
        },
        {
            "Effect": "Allow",
            "Action": [
                "elasticloadbalancing:DeregisterInstancesFromLoadBalancer",
                "elasticloadbalancing:DescribeInstanceHealth",
                "elasticloadbalancing:DescribeLoadBalancerAttributes",
                "elasticloadbalancing:DescribeLoadBalancers",
                "elasticloadbalancing:RegisterInstancesWithLoadBalancer",
                "autoscaling:Describe*",
                "autoscaling:UpdateAutoScalingGroup",
                "autoscaling:EnterStandby",
                "autoscaling:ExitStandby"
            ],
            "Resource": "*"
        }
    ]
}

```
