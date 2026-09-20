# Why Infrastructure as Code (IaC)?

Before the advent of IaC, managing infrastructure was a manual, time-consuming, and error-prone process. Infrastructure as Code transforms this by allowing you to define, provision, and manage your cloud resources using human-readable, version-controlled configuration files.

[![TERRAFORM - DEEP DIVE SESSIONS IN ENGLISH - SESSION 1 - INFRASTRUCTURE AS CODE](https://img.youtube.com/vi/C0tcsXdyeZ4/0.jpg)](https://youtu.be/C0tcsXdyeZ4)

### The Shift: Manual vs. IaC

Here is a breakdown of the challenges faced by system administrators before IaC, and how modern tools resolve them:

| Challenge | Before IaC (Manual Management) | The IaC Solution |
| --- | --- | --- |
| **Configuration** | Servers set up by hand, leading to "snowflake" servers with untracked inconsistencies. | **Automated & Consistent:** Infrastructure is provisioned exactly as defined in the code, every time. |
| **Version Control** | Configurations lived in administrators' heads; rolling back meant manual untangling. | **Git-Backed:** Code is version-controlled. Teams can review PRs, track history, and revert instantly. |
| **Documentation** | Heavy reliance on runbooks and wikis that quickly became outdated. | **Self-Documenting:** The code itself acts as the single source of truth for the environment's state. |
| **Speed & Scale** | Provisioning environments took days or weeks of clicking through console menus. | **Rapid Provisioning:** Whole environments (Dev, Staging, Prod) can be spun up or destroyed in minutes. |

[![TERRAFORM IN TAMIL - DAY 1 PART 2 - INFRASTRUCTURE AS CODE](https://img.youtube.com/vi/c6m5w48hTJA/0.jpg)](https://youtu.be/c6m5w48hTJA)

### Visualizing the Difference: Provisioning a Server

**The Old Way (Manual Clicks):**

1. Log into the AWS Management Console.
2. Navigate to EC2 -> Click "Launch Instance".
3. Search for and select an AMI.
4. Select the `t2.micro` instance type.
5. Click through networking, storage, and tagging menus.
6. Configure Security Groups.
7. Click "Launch" and hope you didn't miss a step.

**The IaC Way (Terraform):**
Instead of clicking through menus, you declare exactly what you want. The IaC tool handles the API calls to make it happen.

```hcl
# Example: Provisioning an AWS Server with Terraform
resource "aws_instance" "web_server" {
  ami           = "ami-0c55b159cbfafe1f0" # Amazon Linux 2
  instance_type = "t2.micro"

  tags = {
    Name        = "Frontend-WebServer"
    Environment = "Production"
    ManagedBy   = "Terraform"
  }
}

```

By adopting tools like **Terraform**, **AWS CloudFormation**, or **Azure Resource Manager**, organizations replace slow, brittle manual processes with a systematic, automated, and code-driven approach to infrastructure.
