# AWS SCP Analysis Tool

## Overview
This Python script is designed to help analyze Service Control Policies (SCPs) within an AWS Organization. It aims to identify AWS services that are blocked or restricted by SCPs, providing valuable insights into the organization’s security and access management settings. This can be especially useful for IT administrators or engineers who need a clear understanding of their organization's permissions structure.

## Features
- **List Active SCP Policies**: Retrieves and lists all active Service Control Policies in the AWS Organization.
- **Identify Blocked AWS Services**: Compares active SCP policies against an exhaustive list of AWS services to identify which services are blocked.
- **IAM Analysis (Future Scope)**: Placeholder function for analyzing IAM policy access restrictions.

## Requirements
- Python 3.x
- Boto3: AWS SDK for Python
- AWS credentials configured (e.g., using `~/.aws/credentials` or environment variables)
- IAM user or role with sufficient permissions to read AWS Organizations SCP policies

## Installation
1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd <repository-directory>
   ```
2. **Install Dependencies**:
   ```bash
   pip install boto3
   ```

## AWS Permissions
The script requires permissions to list and describe SCPs. Ensure that the IAM role or user running the script has the following AWS permissions:
- `organizations:ListPolicies`
- `organizations:DescribePolicy`

## Usage
1. **Set up AWS Credentials**:
   Ensure that your AWS credentials are properly configured. You can set this up using the AWS CLI:
   ```bash
   aws configure
   ```
2. **Run the Script**:
   Execute the script using Python:
   ```bash
   python aws_scp_analysis.py
   ```

### Sample Output
The script will output the list of AWS services that are blocked by active SCPs within your AWS account. For example:

```
The following AWS services are blocked by SCPs in your account:
- ec2
- s3
- rds
```

If no services are blocked, you will see:
```
No AWS services are blocked by SCPs in your account.
```

## Script Breakdown

### Importing Required Libraries
```python
import boto3
from botocore.exceptions import ClientError
```
This script uses Boto3, the official AWS SDK for Python, to interact with AWS services.

### Initialization
The script initializes two boto3 clients: 
- `org_client` for AWS Organizations
- `iam_client` for IAM (though the IAM part is currently a placeholder).

### AWS Services List
The script maintains an exhaustive list of AWS services, which are used to determine which services are blocked by SCPs.

### Function Definitions
- **`get_active_scp_policies()`**:
  - Lists all SCPs in the AWS Organization.
  - Returns only the active SCPs.
  
- **`get_aws_services_blocked_by_scp(scps)`**:
  - Identifies which AWS services are blocked by the given SCPs.
  - Returns a list of blocked services.

- **`list_iam_access_restrictions()`**:
  - A placeholder function for future IAM policy analysis.

### Main Function
- **`main()`**:
  - Retrieves all active SCPs.
  - If no SCPs are found, it prints a message.
  - If SCPs are found, it proceeds to identify blocked AWS services and prints them.

## Future Improvements
- **IAM Analysis**: Extend functionality to analyze IAM policies to identify restrictions or allow permissions at a granular level.
- **Enhanced SCP Parsing**: Improve the method used to parse SCP content to accurately evaluate conditions, actions, and other policy elements.

## Troubleshooting
- **Access Denied Errors**: Ensure the AWS credentials used have sufficient permissions to access AWS Organizations.
- **Empty Output**: If no SCPs are listed, ensure SCPs are enabled in your AWS Organization and the user has proper permissions.

## Contributing
Feel free to contribute by submitting pull requests or opening issues for feature requests, bugs, or improvements.

## License
This project is licensed under the MIT License. See the `LICENSE` file for more details.

## Disclaimer
This script is provided as-is and is intended for informational and educational purposes. Use at your own risk, and always test in a safe environment before running it in production.

---

By using this script, users can gain better visibility into the policies that control their AWS environments, which is crucial for maintaining security, compliance, and operational efficiency.
