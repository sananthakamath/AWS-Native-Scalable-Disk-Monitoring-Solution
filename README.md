## AWS-Native-Scalable-Disk-Monitoring-Solution
This a repository containing the artifacts on the Disk Monitoring Solution I designed.



## Overview

This solution replaces **Ansible-based disk monitoring** with a fully AWS-native architecture using **AWS Systems Manager (SSM)**, **Amazon CloudWatch**, and **AWS Organizations**. It operates on a **hub-and-spoke model** for enterprise-scale, zero-touch monitoring across multiple accounts and regions.

## Architecture

- **Hub** — Central Monitoring Account (Delegated Admin) hosts OAM Sink, CloudWatch Dashboard, SNS Topics, and EventBridge Rules
- **Spokes** — Member accounts in OUs receive auto-deployed monitoring stacks
- **Governance** — Management Account owns the Organization structure, SCPs, and StackSets
- Requires only **HTTPS outbound (port 443)** — no SSH, bastion hosts, or open inbound ports

## Five Core Components

1. **Access & Identity Management** — IAM Instance Profiles with `aws:PrincipalOrgID` for org-wide trust; SCPs prevent disabling monitoring
2. **Data Collection & Aggregation** — CloudWatch Agent collects disk metrics (`used_percent`, `free`, `total`, `inodes_free`) every 60 seconds to a custom namespace
3. **Scalability via Service-Managed StackSets** — Targets OUs for zero-touch auto-deployment to new accounts; SSM State Manager associations enroll all EC2 instances automatically
4. **Centralized Dashboard & Observability (OAM)** — OAM Sink aggregates metrics from all spoke accounts/regions with heatmaps, anomaly detection, and Top-N views
5. **Alerting & EventBridge Organization Rules** — Warning (>85%) and Critical (>95%) alarms routed via a single EventBridge Organization rule to a central SNS topic

## Key Advantages Over Ansible

- No SSH keys, bastion hosts, or dedicated Ansible Tower/AWX infrastructure
- Zero-touch onboarding when accounts join the Production OU
- SCP-enforced compliance — monitoring can't be disabled even by account admins
- Self-healing via SSM State Manager drift detection
- Complete audit trail via CloudTrail

## Cost

**~$200–300/month for 500 VMs across 5 accounts and 3 regions** — most core components (SSM Agent, State Manager, Organizations, OAM) are free. The primary costs are CloudWatch custom metrics (~$0.30/metric) and alarms ($0.10/alarm).
