**Service-Managed StackSet CloudFormation Template**

Deploy this template as a service-managed StackSet from the Management Account (or Delegated Administrator account), targeting the Production OU with automatic deployments enabled. It will deploy to all current member accounts and any future accounts that join the OU.

**SSM State Manager Associations (CloudFormation YAML)**

These two associations are deployed into every spoke account and region via the StackSet. The first installs the CloudWatch Agent package; the second applies the disk monitoring configuration from Parameter Store. By targeting InstanceIds: "*", they catch all current and future EC2 instances automatically.

