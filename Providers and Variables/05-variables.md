# Variables

Input and output variables in Terraform are essential for parameterizing and sharing values within your Terraform configurations and modules. They allow you to make your configurations more dynamic, reusable, and flexible.

Terraform variables are a way to store values that can be reused throughout your Terraform configuration.

They allow you to define a value once and reference it in multiple places throughout your configuration, making it easier to manage and update your infrastructure.

## Input Variables

Input variables are used to parameterize your Terraform configurations. They allow you to pass values into your modules or configurations from the outside. Input variables can be defined within a module or at the root level of your configuration. Here's how you define an input variable:

```hcl
variable "example_var" {
  description = "An example input variable"
  type        = string
  default     = "default_value"
}
```

In this example:

- `variable` is used to declare an input variable named `example_var`.
- `description` provides a human-readable description of the variable.
- `type` specifies the data type of the variable (e.g., `string`, `number`, `list`, `map`, etc.).
- `default` provides a default value for the variable, which is optional.

Variables are defined in the variables block in your Terraform configuration file, where you can give a name and a default value. Please refer to the following screenshot exaplaining how variables are defined inside terraform-

<img width="1591" height="252" alt="image" src="https://github.com/user-attachments/assets/fc0a3523-e9d1-48cf-aca6-2af570ba2d32" />


You can then use the input variable within your module or configuration like this:

```hcl
resource "example_resource" "example" {
  name = var.example_var
  # other resource configurations
}
```

You reference the input variable using `var.example_var`.


* Terraform variables can have various type such as string, number, boolean, list, map etc.
* Variables can be set in the command line when running Terraform commands using the -var flag.
* Variables can also be set using a separate file, called a variable file, using the -var-file flag.
* Variables can be accessed in Terraform configuration files using the var function, for example var.example_variable
* Variables are useful for storing values that may change between environments, for example, different values for test and production environments.


## Output Variables

Output variables allow you to expose values from your module or configuration, making them available for use in other parts of your Terraform setup. Here's how you define an output variable:

```hcl
output "example_output" {
  description = "An example output variable"
  value       = resource.example_resource.example.id
}
```

In this example:

- `output` is used to declare an output variable named `example_output`.
- `description` provides a description of the output variable.
- `value` specifies the value that you want to expose as an output variable. This value can be a resource attribute, a computed value, or any other expression.

You can reference output variables in the root module or in other modules by using the syntax `module.module_name.output_name`, where `module_name` is the name of the module containing the output variable.

For example, if you have an output variable named `example_output` in a module called `example_module`, you can access it in the root module like this:

```hcl
output "root_output" {
  value = module.example_module.example_output
}
```

This allows you to share data and values between different parts of your Terraform configuration and create more modular and maintainable infrastructure-as-code setups.
