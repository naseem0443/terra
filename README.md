
## Terraform Mock  Exam 1

**1. What is Immutable Infrastructure?**


* [ ] Resources once deployed are not intended to be changed
* [ ] Resources cannot be migrated to another platform
* [ ] Any aspect of a resource can be updated in place anytime 
* [ ] Resources strictly provisioned by Terraform

**Correct answer:**
* [x] Resources once deployed are not intended to be changed

**Explaination**: Immutable infrastructure is another paradigm in which it ensures that resources are never modified after they have been deployed.
If a change is to be made, a new instance of that resource will be provisioned in place of the old one.

**2. What does “IaC” stand for?**


* [ ] Infrastructure as Code
* [ ] Initialization as Code
* [ ] Code as Infrastructure
* [ ] None of the above

**Correct answer:**
* [x] Infrastructure as Code

**Explaination**: IaC stands for Infrastructure as Code.

**3. Select the file extension used by terraform configuration files.**


* [ ] .TF
* [ ] .YAML
* [ ] .TOML
* [ ] .DAT
* [ ] None of the Above

**Correct answer:**
* [x] .TF

**4. Choose the correct terraform command to display the blueprint of the infrastructure to be applied.**


* [ ] terraform init
* [ ] terraform apply
* [ ] terraform plan
* [ ] terraform show

**Correct answer:**
* [x] terraform plan

**5. Your team assigned you the task of developing a terraform configuration to provision a bunch of services on GCP. You did everything to the point but forgot to mention the provider's version in the terraform block. What default behavior would you expect from terraform:**


* [ ] a. Terraform init will fail
* [ ] b. Terraform will download and use the latest version of providers used in the configuration
* [ ] c. Terraform init will succeed but an apply will fail because of unsupported provider versions
* [ ] d. None of the above
* [ ] e. All of the above

**Correct answer:**
* [x] b. Terraform will download and use the latest version of providers used in the configuration

**Explaination**: Terraform will download the latest version for all the providers used within the configuration. The version downloaded may or may not work well with the configuration developed. 

**6. Which "terraform command"  from the following downloads the latest version of the provider plugins?**


* [ ] terraform plan
* [ ] terraform init
* [ ] terraform apply
* [ ] terraform pull

**Correct answer:**
* [x] terraform init

**Documentation Link**: https://www.terraform.io/docs/cli/commands/init.html

**7. The label after the variable keyword should be unique among all variables.**


* [ ] a. Should be unique among the variables in the same module
* [ ] b.You can create just two variables of the same label
* [ ] Both the statements (a) and (b) are true
* [ ] None of the above

**Correct answer:**
* [x] a. Should be unique among the variables in the same module

**Explaination**: A variable name or a label must be unique within the same module or configuration. 

**Documentation Link**: https://www.terraform.io/docs/language/values/variables.html#declaring-an-input-variable

**8. A simple terraform configuration file is given below. What is the name of the resource that will be created?**


* [ ] pet
* [ ] local_file
* [ ] pets.txt
* [ ] local

**Correct answer:**
* [x] pet

**Code**: 
resource "local_file" "pet" {​
  filename = "/root/pets.txt"​
  content = "We love pets!"​ ​
}


**Explaination**: The name of the resource is "pet" which is a local_file type resource.

**9. We just created an environment variable named “TF_VAR_content=foo-3” and ran the following command: `terraform apply -var "content=foo-4"`  .Determine the content of file foo.txt**


* [ ] foo-4
* [ ] foo-3
* [ ] foo
* [ ] foo-1

**Correct answer:**
* [x] foo-4

**Code**: 
resource "local_file" "foo" {
  content  = var.content
  filename = “/random/foo.txt”
}

variable "content" {
  type        = string
  description = "Content of the file to be created"

  validation {
    condition     = substr(var.content, 0, 4) == "foo-"
    error_message = "The content value must be a valid word starting \"foo-\"."
  }
}


**Explaination**: The variables passed with the -var or -var-file command line flags have the highest priority and will take precedence over environment variables. As such, the file will be created with "foo-4" as the content.

**Documentation Link**: https://www.terraform.io/docs/language/values/variables.html#variable-definition-precedence

**10. A variable block is given below. Inspect it and choose the valid options.**


* [ ] Invalid. We cannot use "providers" as a variable name
* [ ] Valid. The "default" argument is optional
* [ ] Invalid. "default" argument is not used
* [ ] Invalid. Incorrect "type" used

**Correct answer:**
* [x] Invalid. We cannot use "providers" as a variable name

**Code**: 
variable "providers" {
  type = string
}

**Explaination**: We can use any name for a variable except for: source,  version, providers, count, for_each, lifecycle, depends_on and locals. 

We have used the variable name as "providers". This is not a valid identifier

**Documentation Link**: https://www.terraform.io/docs/language/values/variables.html#declaring-an-input-variable

**11. Where can we make use of version constraints?**


* [ ] a. Modules
* [ ] b. Provider requirements
* [ ] c. The required_version setting in the terraform block
* [ ] d. All of the above

**Correct answer:**
* [x] d. All of the above

**Explaination**: Version constraints can be used anywhere terraform allows us to specify versions. Most commonly they can be set at:

1. Within the provider version configuration (Inside the required_providers block nested inside the terraform block)
2. The "required_version" argument which is used to set the version of Terraform to use.
3. Within modules. This is where we specify the version of module to be used. 

**Documentation Link**: https://www.terraform.io/docs/language/expressions/version-constraints.html

**12. Observe the below code and determine the providers used.**


* [ ] Local_file and random_pet
* [ ] Pet_name and my-pet
* [ ] Local and random
* [ ] Local_file, random_pet, pet_name, my-pet

**Correct answer:**
* [x] Local and random

**Code**: 
resource "local_file" "pet_name" {
            content = "We love pets!"
            filename = "/root/pets.txt"
}
resource "random_pet" "my-pet" {
              prefix = "Mrs"
              separator = "."
              length = "1"
}


**13. Inspect the below code block and determine the resource attribute that creates a dependency between the given resources.**


* [ ] aws_subnet.cidr_block
* [ ] aws_vpc.cidr_block
* [ ] aws_vpc.backend-vpc.id
* [ ] aws_vpc.backend_vpc.cidr_block
* [ ] aws_subnet.private-subnet1.cidr_block

**Correct answer:**
* [x] aws_vpc.backend-vpc.id

**Code**: 
resource "aws_vpc" "backend-vpc" {
  cidr_block = "10.0.0.0/16"
  tags = {
    Name = "backend-vpc"
  }
}
resource "aws_subnet" "private-subnet1" {
  vpc_id     = aws_vpc.backend-vpc.id
  cidr_block = "10.0.2.0/24"
  tags = {
    Name = "private-subnet1"
  }
}

**Explaination**: The aws_subnet type resource called private-subnet1 makes use of the resource attribute "aws_vpc.backend-vpc.id". 

**14. What is the generic way to reference attributes within the terraform expression?**


* [ ] None of the above
* [ ] RESOURCE_TYPE.ATTRIBUTE.NAME
* [ ] RESOURCE_TYPE.NAME.ATTRIBUTE
* [ ] RESOURCE_TYPE.NAME

**Correct answer:**
* [x] RESOURCE_TYPE.NAME.ATTRIBUTE

**Documentation Link**: https://www.terraform.io/docs/language/expressions/references.html#resources

**15. Whenever the target APIs change or when new functionality is added, the provider maintainers may update new versions for a provider. This may lead to unexpected infrastructure changes. What is the best approach to overcome this?**


* [ ] Never touch what you don’t understand
* [ ] Use required_providers block to clearly define the provider version you want to use
* [ ] API changes does not affect the provider usage within terraform
* [ ] There would be no issue as terraform always downloads the latest version of the provider

**Correct answer:**
* [x] Use required_providers block to clearly define the provider version you want to use

**Explaination**: The functionality of a provider plugin may vary drastically from one version to another. 
Our terraform configuration may not work as expected when using a version different than the one it was written in. As a best practice, always declare the exact version of the provider we want to use within the required_providers block.


**16. Which keyword is reserved for declaring variables in the terraform configuration files?**


* [ ] variable
* [ ] var
* [ ] Use the syntax var.<variable_name>
* [ ] variable block does not need a keyword
* [ ] user-defined keyword

**Correct answer:**
* [x] variable

**Explaination**: The variable block begins with the "variable" keyword followed by a user defined name/label for the variable. 

**Documentation Link**: https://www.terraform.io/docs/language/values/variables.html#declaring-an-input-variable

**17. Each output value exported by a module must be declared using an ______ block.**


* [ ] output 
* [ ] input
* [ ] variable
* [ ] resource
* [ ] data

**Correct answer:**
* [x] output 

**Documentation Link**: https://www.terraform.io/docs/language/values/outputs.html#declaring-an-output-value

**18. Select the optional arguments that are available for the output block.**


* [ ] description
* [ ] sensitive
* [ ] depends_on
* [ ] All of the above

**Correct answer:**
* [x] All of the above

**Documentation Link**: https://www.terraform.io/docs/language/values/outputs.html#optional-arguments

**19. Name the file that is created by default when you run the `terraform apply` command for the first time**


* [ ] terraform.state
* [ ] state.tf
* [ ] terraform.tf
* [ ] terraform.tfstate

**Correct answer:**
* [x] terraform.tfstate

**20. We have a local file resource with certain content. Once this resource is provisioned, the file is created in the `/root` directory and the information about this file is also stored in the Terraform state file. Now let's create a new file using a simple shell script in the same directory `/root`. Quite evidently, this file is outside the control and management of Terraform at this point in time. How would you include the second file in your Terraform configuration?**


* [ ] By creating a resource type object inside the main.tf file.
* [ ] By creating a data type object inside the main.tf file
* [ ] Terraform automatically syncs the files under the same directory
* [ ] Terraform doesn't provide such functionality

**Correct answer:**
* [x] By creating a data type object inside the main.tf file

**21. What steps are needed in order to change the backend in terraform? For instance : local to remote**


* [ ] Adding a terraform block only, would be enough
* [ ] Add a backend block within a terraform block
* [ ] Specifying the backend block within the terraform block is followed by reinitialization of the backend using `terraform init`.
* [ ] Any one of the options is enough.

**Correct answer:**
* [x] Specifying the backend block within the terraform block is followed by reinitialization of the backend using `terraform init`.

**22. Choose the meta-argument which is not supported by the data block.**


* [ ] depends_on
* [ ] count
* [ ] for_each
* [ ] provider
* [ ] lifecycle

**Correct answer:**
* [x] lifecycle

**23. Which command can be used to create a visual representation of our terraform resources?**


* [ ] terraform view
* [ ] terraform console
* [ ] terraform map
* [ ] terraform graph

**Correct answer:**
* [x] terraform graph

**24. `terraform plan` and `terraform apply` both refresh the state before their execution. Which option could be used to disable this default behaviour?**


* [ ] -refresh=disable
* [ ] -refresh=no
* [ ] -refresh=false
* [ ] -no-refresh=true

**Correct answer:**
* [x] -refresh=false

**25. Every terraform command listed is useful for inspecting infrastructure:- `output`, `graph`, `show`, `state list`, `state show`**


* [ ] True
* [ ] False

**Correct answer:**
* [x] True

**26. You wanted to play with terraform to check what it has to offer. After a while you remembered that you didn’t specify any configuration for the backend. What default behaviour is expected here of terraform?**


* [ ] Terraform will use a local backend, which requires no configuration
* [ ] Terraform will use a remote backend, which requires no configuration.
* [ ] Terraform will randomly use a backend from a pool of local or remote ones
* [ ] None of the above

**Correct answer:**
* [x] Terraform will use a local backend, which requires no configuration

**27. We can delete the `default` terraform workspace.**


* [ ] True
* [ ] False

**Correct answer:**
* [x] False

**28. Can you export the debug logs from `terraform` only by setting the `TF_LOG_PATH` environment variable?**


* [ ] True
* [ ] False

**Correct answer:**
* [x] False

**29. Which of the following is not the valid sub-command of `terraform state` command?**


* [ ] state mv
* [ ] state list
* [ ] state show
* [ ] state pull
* [ ] state rm
* [ ] state replace

**Correct answer:**
* [x] state replace

**30. For local state, Terraform stores the workspace states in a directory called :**


* [ ] terraform.tfstate
* [ ] terraform.tfstate.d
* [ ] tfstate.d
* [ ] None of the above

**Correct answer:**
* [x] terraform.tfstate.d

**31. Every initialized working directory has at least one workspace.**


* [ ] True
* [ ] False

**Correct answer:**
* [x] True

**32. Which environment variable is exported to set a different log level in the terraform?**


* [ ] TF_LOG
* [ ] var.TF_LOG
* [ ] VAR_TF_LOG
* [ ] TF_LOG_PATH

**Correct answer:**
* [x] TF_LOG

**33. Select the types of terraform modules based on the credibility tier.**


* [ ] Verified
* [ ] Non-verified
* [ ] Official 
* [ ] Community

**Correct answer:**
* [x] Verified
* [x] Community
* [x] Official 

**34. You intend to import two resources to your terraform configuration. You executed only the `terraform import` command until now and it worked. Will the `terraform apply` work if executed now?**


* [ ] It will throw an error
* [ ] Works like a charm
* [ ] We haven’t updated the resource with correct argument values yet
* [ ] None of the options

**Correct answer:**
* [x] It will throw an error
* [x] We haven’t updated the resource with correct argument values yet

**35. A given resource or module block cannot use both `count` and `for_each` simultaneously.**


* [ ] True
* [ ] False

**Correct answer:**
* [x] True

**36. Modules can also call other modules using a _________ block**


* [ ] modules
* [ ] module
* [ ] Only the root module can call other modules
* [ ] None of the above

**Correct answer:**
* [x] module

**37. The for_each meta-argument accepts:**


* [ ] map 
* [ ] set of strings
* [ ] list of strings
* [ ] Only alphanumeric characters

**Correct answer:**
* [x] map 
* [x] set of strings

**38. Fill the blank with the suitable choice:**


* [ ] destroy
* [ ] create
* [ ] apply
* [ ] plan 

**Correct answer:**
* [x] destroy

**Code**: 
resource "aws_instance" "web" {
  # ...

  provisioner "local-exec" {
    when    = ________
    command = "echo 'Destroy-time provisioner'"
  }
}


**39. Where should you add a `provisioner` block?**


* [ ] Nested block inside the resource block
* [ ] Outside the resource block
* [ ] Nested block inside the provider block
* [ ] Inside the terraform block

**Correct answer:**
* [x] Nested block inside the resource block

**40. Which argument of the lifecycle meta-argument supports a list as a value ?**


* [ ] create_before_destroy
* [ ] ignore_changes 
* [ ] prevent_destroy 
* [ ] All the options

**Correct answer:**
* [x] ignore_changes 

**Explaination**: ignore_changes (list of attribute names) - By default, Terraform detects any difference in the current settings of a real infrastructure object and plans to update the remote object to match configuration.

**41. Select the types of provisioners available:**


* [ ] local-exec
* [ ] remote-exec
* [ ] file
* [ ] all of the above

**Correct answer:**
* [x] all of the above

**42. What happens when provisioners fail to execute successfully?**


* [ ] Terraform will taint the resource that will be replaced on the next run
* [ ] Resources will be created but without the changes mentioned in the provisioner block
* [ ] It will show an error message showing the user to taint the resource manually
* [ ] None of the above

**Correct answer:**
* [x] Terraform will taint the resource that will be replaced on the next run

**43. Which statement best explains terraform provisioners?**


* [ ] used to model specific actions only on the local machine
* [ ] used to model specific actions only on the remote machine
* [ ] used to model specific actions on the local machine or on a remote machine
* [ ] None of the above

**Correct answer:**
* [x] used to model specific actions on the local machine or on a remote machine

**44. Select the available arguments that are available for the lifecycle meta-argument**


* [ ] create_before_destroy
* [ ] ignore_change
* [ ] prevent_destroy
* [ ] ignore_changes
* [ ] destroy_after_create

**Correct answer:**
* [x] create_before_destroy
* [x] prevent_destroy
* [x] ignore_changes

**45. Chose the option that  best describes “in-place updates”:**


* [ ] The underlying infrastructure remains the same
* [ ] Software and configuration of operating system changes as part of the update
* [ ] Both 
* [ ] Neither

**Correct answer:**
* [x] Both 

**46. Inspect the following code and select what will happen if we run a terraform init for this configuration:**


* [ ] Valid code. Terraform init will work
* [ ] Invalid default value for variable
* [ ] Invalid default value but terraform will convert the value to the type specified
* [ ] None of the above

**Correct answer:**
* [x] Invalid default value for variable

**Code**: 
variable "is_true" {
    type = bool
    default = 1
}

**Explaination**: The default value for this variable is a number and the type is set to a boolean. Terraform init will fail with an error as shown below:

------------------------------------------------------------------------------------------------------------------------
The Terraform configuration must be valid before initialization so that
Terraform can determine which modules and providers need to be installed.

Error: Invalid default value for variable

  on variables.tf line 20, in variable "istrue":
  20:     default = 1

This default value is not compatible with the variable's type constraint: bool
required.
------------------------------------------------------------------------------------------------------------------------

**47. The Terraform language supports user-defined functions**


* [ ] True
* [ ] False

**Correct answer:**
* [x] False

**48. General syntax for function calls is :**


* [ ] Function name followed by comma-separated arguments in parentheses.
* [ ] Function name followed by space-separated arguments in parentheses
* [ ] Both
* [ ] None

**Correct answer:**
* [x] Function name followed by comma-separated arguments in parentheses.

**49. Which of the following can be used to determine the length of a given list, map, or string.**


* [ ] length()
* [ ] len()
* [ ] size()
* [ ] count()

**Correct answer:**
* [x] length()

**50. Select the options that does not support dynamic block:**


* [ ] provisioner
* [ ] provider
* [ ] dynamic
* [ ] data
* [ ] resource
* [ ] locals

**Correct answer:**
* [x] locals

**Explaination**: A dynamic block can only generate arguments that belong to the resource type, data source, provider or provisioner being configured. It is not possible to generate meta-argument blocks such as lifecycle and provisioner blocks , since Terraform must process these before it is safe to evaluate expressions.

**51. Can we use `dynamic` blocks to generate `meta-argument` blocks such as `lifecycle` and `provisioner` blocks?**


* [ ] True
* [ ] False

**Correct answer:**
* [x] False

**Explaination**: A dynamic block can only generate arguments that belong to the resource type, data source, provider, or provisioner being configured. It is not possible to generate meta-argument blocks such as lifecycle and provisioner blocks, since Terraform must process these before it is safe to evaluate expressions.

**52. By default terraform cloud runs terraform on:**


* [ ] its own cloud infrastructure
* [ ] on your own isolated, private, or on-premises infrastructure
* [ ] You need to specify each time you run terraform commands
* [ ] None of the above

**Correct answer:**
* [x] its own cloud infrastructure

**53. Passing an object containing a sensitive input variable to the keys() function will result in a list that is _________ .**


* [ ] Sensitive
* [ ] Non-sensitive
* [ ] Random output
* [ ] None of the above.

**Correct answer:**
* [x] Sensitive

**54. “alias” and “version” are the `meta-arguments` which are available for all provider blocks?**


* [ ] True
* [ ] False

**Correct answer:**
* [x] True

**55. Select the workflows that `Terraform cloud` utilizes to manage Terraform runs:**


* [ ] UI/VCS-driven run workflow
* [ ] API-driven run workflow
* [ ] CLI-driven run workflow
* [ ] None of the above

**Correct answer:**
* [x] UI/VCS-driven run workflow
* [x] API-driven run workflow
* [x] CLI-driven run workflow

**56. In the UI and VCS workflow, every workspace is associated with a specific branch of a VCS repo of Terraform configurations.**


* [ ] True
* [ ] False

**Correct answer:**
* [x] True

**Explaination**: In the UI and VCS workflow, every workspace is associated with a specific branch of a VCS repo of Terraform configurations. Terraform Cloud registers webhooks with your VCS provider when you create a workspace, then automatically queues a Terraform run whenever new commits are merged to that branch of workspace's linked repository.

**57. Is `Terraform Cloud workspaces` same as `Terraform CLI Workspaces`.**


* [ ] Yes
* [ ] No

**Correct answer:**
* [x] No

**58. `terraform import` command updates the configuration files as well as the state file, with the details of the infrastructure being imported.**


* [ ] True 
* [ ] False

**Correct answer:**
* [x] False

**59. What is `Sentinel`?**


* [ ] Policy as code framework for HashiCorp Enterprise Products
* [ ] Infrastructure as code framework for Terraform
* [ ] Both 
* [ ] None of the above

**Correct answer:**
* [x] Policy as code framework for HashiCorp Enterprise Products

**60. You were working with different terraform scripts which are provisioning various sets of resources , you need to look up for some additional details related to one specific resource from the state file. Which `terraform command` will help you achieve this?**


* [ ] terraform state list ADDRESS
* [ ] terraform state show ADDRESS
* [ ] terraform show ADDRESS
* [ ] terraform get ADDRESS

**Correct answer:**
* [x] terraform state show ADDRESS
