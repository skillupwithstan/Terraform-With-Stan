Here is the fully formatted Markdown file. You can easily copy this entire block and save it as your `.md` file. All the code sections are properly enclosed in syntax-highlighted blocks to preserve their alignment and make them easy to copy.

```markdown
# 1. Types of Terraform Variables

There are two types of variables in Terraform:
* Simple values
* Collection Variable

## 1.1 Simple Values variables
As the name suggests, Simple Values variables are those which hold only a single value. Here are the types of Simple Value variables:
* string
* number
* bool

## 1.2 Collection Variable
In the collection variable, it consists of:
* List
* Map
* Set

---

# 2. Terraform Variables - string, number, bool

Let's take a simple example in which we are going to set up an EC2 instance on AWS. So, to create an EC2 instance we need two things:
* provider
* resource

Here is the `main.tf` which we are going to parameterize using terraform variables.

```hcl
provider "aws" {
  region     = "eu-central-1"
  access_key = "<INSERT_YOUR_ACCESS_KEY>"
  secret_key = "<INSERT_YOUR_SECRET_KEY>"
}

resource "aws_instance" "ec2_example" {
  ami           = "ami-0767046d1677be5a0"
  instance_type = "t2.micro"
  tags = {
    Name = "Terraform EC2"
  }
}

```

## 2.1 string variable type - We are going to parameterize `instance_type = "t2.micro"`

The first rule to create a parameter in a terraform file is by defining a variable block.
Example:

```hcl
variable "instance_type" {
  description = "Instance type t2.micro"
  type        = string
  default     = "t2.micro"
}

```

For defining a variable block you need:

* **description:** Small or short description about the purpose of the variable.
* **type:** What type of variable it is going to be (e.g., string, bool, number...).
* **default:** What would be the default value of the variable.

Let's replace the hardcoded value of `instance_type` with the variable:

```hcl
instance_type = var.instance_type

```

Here is our final terraform file after replacing the hardcoded value with a variable:

```hcl
provider "aws" {
  region     = "eu-central-1"
  access_key = "<INSERT_YOUR_ACCESS_KEY>"
  secret_key = "<INSERT_YOUR_SECRET_KEY>"
}

resource "aws_instance" "ec2_example" {
  ami           = "ami-0767046d1677be5a0"
  instance_type = var.instance_type
  tags = {
    Name = "Terraform EC2"
  }
}

variable "instance_type" {
  description = "Instance type t2.micro"
  type        = string
  default     = "t2.micro"
}

```

And now you can apply your terraform configuration:

```bash
terraform apply

```

## 2.2 number variable type - We are going to parameterize `instance_count = 2`

The next variable type we are going to take is number. For example, we are going to increase the `instance_count` of the ec2_instances.

Let's create the variable first:

```hcl
variable "instance_count" {
  description = "EC2 instance count"
  type        = number
  default     = 2
} 

```

Here is the final terraform file with the instance count:

```hcl
provider "aws" {
  region     = "eu-central-1"
  access_key = "<INSERT_YOUR_ACCESS_KEY>"
  secret_key = "<INSERT_YOUR_SECRET_KEY>"
}

resource "aws_instance" "ec2_example" {
  ami           = "ami-0767046d1677be5a0"
  instance_type = "t2.micro"
  count         = var.instance_count
  tags = {
    Name = "Terraform EC2"
  }
}

variable "instance_count" {
  description = "EC2 instance count"
  type        = number
  default     = 2
}

```

## 2.3 boolean variable type - We are going to parameterize `enable_public_ip = false`

The next variable type which we are going to discuss is bool. The bool variable can be used to set true or false values inside your terraform file.

Here is an example to create your bool variable:

```hcl
variable "enable_public_ip" {
  description = "Enable public IP address"
  type        = bool
  default     = true
}

```

Let's create a complete terraform file with the bool variable:

```hcl
provider "aws" {
  region     = "eu-central-1"
  access_key = "<INSERT_YOUR_ACCESS_KEY>"
  secret_key = "<INSERT_YOUR_SECRET_KEY>"
}

resource "aws_instance" "ec2_example" {
  ami                         = "ami-0767046d1677be5a0"
  instance_type               = "t2.micro"
  count                       = 1
  associate_public_ip_address = var.enable_public_ip
  tags = {
    Name = "Terraform EC2"
  }
}

variable "enable_public_ip" {
  description = "Enable public IP address"
  type        = bool
  default     = true
}

```

---

# 3. Terraform Variables - list, set, map

When it comes to collection input variables, then we are talking about:

* List
* Map
* Set

## 3.1 List variable type

As the name suggests, we are going to define a list that will contain more than one element in it.

Let's define our first List variable. Here is the list of IAM users:

```hcl
variable "user_names" {
  description = "IAM usernames"
  type        = list(string)
  default     = ["user1", "user2", "user3s"]
}

```

Here is our final terraform file with List variables:

```hcl
provider "aws" {
  region     = "eu-central-1"
  access_key = "<INSERT_YOUR_ACCESS_KEY>"
  secret_key = "<INSERT_YOUR_SECRET_KEY>"
}

resource "aws_instance" "ec2_example" {
  ami           = "ami-0767046d1677be5a0"
  instance_type = "t2.micro"
  count         = 1
  tags = {
    Name = "Terraform EC2"
  }
}

resource "aws_iam_user" "example" {
  count = length(var.user_names)
  name  = var.user_names[count.index]
}

variable "user_names" {
  description = "IAM usernames"
  type        = list(string)
  default     = ["user1", "user2", "user3s"]
}

```

## 3.2 Map variable type

Terraform also supports the map variable type where you can define key-value pairs.
Let's take an example where we need to define a project and an environment. We can use the map variable to achieve that.

Here is an example of a map variable:

```hcl
variable "project_environment" {
  description = "project name and environment"
  type        = map(string)
  default     = {
    project     = "project-alpha",
    environment = "dev"
  }
}

```

Let's create a Terraform file utilizing this map:

```hcl
provider "aws" {
  region     = "eu-central-1"
  access_key = "<INSERT_YOUR_ACCESS_KEY>"
  secret_key = "<INSERT_YOUR_SECRET_KEY>"
}

resource "aws_instance" "ec2_example" {
  ami           = "ami-0767046d1677be5a0"
  instance_type = "t2.micro"
  tags          = var.project_environment
}

variable "project_environment" {
  description = "project name and environment"
  type        = map(string)
  default     = {
    project     = "project-alpha",
    environment = "dev"
  }
}

```

```

```
