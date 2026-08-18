**CloudWatch Agent Configuration (JSON)**

This configuration is stored centrally in SSM Parameter Store as AmazonCloudWatch-DiskMonitoring in each active region. The agent pulls the config on startup and whenever SSM State Manager re-applies the association.

