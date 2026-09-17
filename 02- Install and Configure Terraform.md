# Install and Configure Terraform

To start provisioning infrastructure, you must first install the Terraform CLI on your local machine and configure it to authenticate with your target cloud provider.

### Step 1: Install the Terraform CLI

The easiest and most reliable way to install Terraform is through your operating system's package manager.

**macOS (using Homebrew)**
Install the official HashiCorp tap and then install Terraform:

```bash
brew tap hashicorp/tap
brew install hashicorp/tap/terraform

```

**Windows (using Chocolatey)**
Open PowerShell as an Administrator and run:

```powershell
choco install terraform

```

*Manual alternative:* Download the Windows executable from the HashiCorp website, extract the `.zip` file, and move the `terraform.exe` binary to a directory included in your system's `PATH` environment variable.

**Linux (Ubuntu/Debian)**
Add the HashiCorp GPG key and repository, then update and install:

```bash
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform

```

### Step 2: Verify the Installation

Once installed, verify that the binary is available on your system's path and check the version. Open a new terminal session and run:

```bash
terraform -version

```

If installed correctly, you will see output similar to `Terraform v1.x.x`.

### Step 3: Configure Cloud Credentials

Installing Terraform only gives you the core engine. To actually create resources, Terraform needs permission to interact with your cloud provider's API.

The most secure and standard way to provide these credentials is by configuring your local environment, rather than hardcoding credentials into your `.tf` files.

**Example: Configuring for AWS**
If you are deploying to Amazon Web Services, Terraform defaults to using the credentials configured via the AWS CLI.

1. Install the AWS CLI for your operating system.
2. Run the configuration command in your terminal:
```bash
aws configure

```


3. Provide your IAM user credentials when prompted:
```text
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-east-1
Default output format [None]: json

```



**Alternative: Environment Variables**
If you do not want to install the cloud provider's CLI, you can export your credentials directly as environment variables in your terminal session. Terraform automatically detects these.

*Linux/macOS:*

```bash
export AWS_ACCESS_KEY_ID="AKIAIOSFODNN7EXAMPLE"
export AWS_SECRET_ACCESS_KEY="wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"
export AWS_REGION="us-east-1"

```

*Windows (PowerShell):*

```powershell
$env:AWS_ACCESS_KEY_ID="AKIAIOSFODNN7EXAMPLE"
$env:AWS_SECRET_ACCESS_KEY="wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY"
$env:AWS_REGION="us-east-1"

```

### Step 4: Developer Environment Enhancements (Recommended)

To make writing and executing Terraform code much easier, set up these two local enhancements:

* **IDE Support:** Install the official **HashiCorp Terraform extension** for Visual Studio Code (or your preferred IDE). This provides syntax highlighting, auto-completion for resource attributes, and automated formatting.
* **Terminal Autocompletion:** Terraform includes a built-in command to enable tab-completion in your shell (Bash or Zsh). Run the following command and restart your terminal:
```bash
terraform -install-autocomplete

```
