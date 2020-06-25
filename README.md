<!-- This file was automatically generated by the `geine`. Make all changes to `README.yaml` and run `make readme` to rebuild this file. -->

<p align="center"> <img src="https://user-images.githubusercontent.com/50652676/62349836-882fef80-b51e-11e9-99e3-7b974309c7e3.png" width="100" height="100"></p>


<h1 align="center">
    Terraform AWS Cloudwatch Alarms
</h1>

<p align="center" style="font-size: 1.2rem;">
    Terraform module creates Cloudwatch Alarm on AWS for monitoriing AWS services.
     </p>

<p align="center">

<a href="https://www.terraform.io">
  <img src="https://img.shields.io/badge/Terraform-v0.12-green" alt="Terraform">
</a>
<a href="LICENSE.md">
  <img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="Licence">
</a>


</p>
<p align="center">

<a href='https://facebook.com/sharer/sharer.php?u=https://github.com/clouddrove/terraform-aws-cloudwatch-alarms'>
  <img title="Share on Facebook" src="https://user-images.githubusercontent.com/50652676/62817743-4f64cb80-bb59-11e9-90c7-b057252ded50.png" />
</a>
<a href='https://www.linkedin.com/shareArticle?mini=true&title=Terraform+AWS+Cloudwatch+Alarms&url=https://github.com/clouddrove/terraform-aws-cloudwatch-alarms'>
  <img title="Share on LinkedIn" src="https://user-images.githubusercontent.com/50652676/62817742-4e339e80-bb59-11e9-87b9-a1f68cae1049.png" />
</a>
<a href='https://twitter.com/intent/tweet/?text=Terraform+AWS+Cloudwatch+Alarms&url=https://github.com/clouddrove/terraform-aws-cloudwatch-alarms'>
  <img title="Share on Twitter" src="https://user-images.githubusercontent.com/50652676/62817740-4c69db00-bb59-11e9-8a79-3580fbbf6d5c.png" />
</a>

</p>
<hr>


We eat, drink, sleep and most importantly love **DevOps**. We are working towards strategies for standardizing architecture while ensuring security for the infrastructure. We are strong believer of the philosophy <b>Bigger problems are always solved by breaking them into smaller manageable problems</b>. Resonating with microservices architecture, it is considered best-practice to run database, cluster, storage in smaller <b>connected yet manageable pieces</b> within the infrastructure.

This module is basically combination of [Terraform open source](https://www.terraform.io/) and includes automatation tests and examples. It also helps to create and improve your infrastructure with minimalistic code instead of maintaining the whole infrastructure code yourself.

We have [*fifty plus terraform modules*][terraform_modules]. A few of them are comepleted and are available for open source usage while a few others are in progress.




## Prerequisites

This module has a few dependencies:

- [Terraform 0.12](https://learn.hashicorp.com/terraform/getting-started/install.html)
- [Go](https://golang.org/doc/install)
- [github.com/stretchr/testify/assert](https://github.com/stretchr/testify)
- [github.com/gruntwork-io/terratest/modules/terraform](https://github.com/gruntwork-io/terratest)







## Examples


**IMPORTANT:** Since the `master` branch used in `source` varies based on new modifications, we suggest that you use the release versions [here](https://github.com/clouddrove/terraform-aws-cloudwatch-alarms/releases).


### Simple Example
Here is an example of how you can use this module in your inventory structure:
```hcl
    module "alarm" {
      source                    = "https://github.com/clouddrove/terraform-aws-cloudwatch-alarms.git?ref=tags/0.12.2"
      name                      = "alarm"
      application               = "clouddrove"
      environment               = "test"
      label_order               = ["environment", "name", "application"]
      alarm_name                = "cpu-alarm"
      comparison_operator       = "LessThanThreshold"
      evaluation_periods        = 2
      metric_name               = "CPUUtilization"
      namespace                 = "AWS/EC2"
      period                    = "60"
      statistic                 = "Average"
      threshold                 = "40"
      alarm_description         = "This metric monitors ec2 cpu utilization"
      alarm_actions             = ["arn:aws:sns:eu-west-1:xxxxxxxxxxx:test"]
      actions_enabled           = true
      insufficient_data_actions = []
      ok_actions                = []
      dimensions                = {
                    instance_id = "i-xxxxxxxxxxxxx"
      }
  }
```






## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| actions\_enabled | Indicates whether or not actions should be executed during any changes to the alarm's state. | bool | `"true"` | no |
| alarm\_actions | The list of actions to execute when this alarm transitions into an ALARM state from any other state. | list | `<list>` | no |
| alarm\_description | The description for the alarm. | string | `""` | no |
| alarm\_name | The descriptive name for the alarm. | string | n/a | yes |
| application | Application \(e.g. `cd` or `clouddrove`\). | string | `""` | no |
| comparison\_operator | The arithmetic operation to use when comparing the specified Statistic and Threshold. | string | n/a | yes |
| dimensions | Dimensions for metrics. | map | `<map>` | no |
| enabled | Enable alarm. | bool | `"true"` | no |
| environment | Environment \(e.g. `prod`, `dev`, `staging`\). | string | `""` | no |
| evaluation\_periods | The number of periods over which data is compared to the specified threshold. | number | n/a | yes |
| instance\_id | The instance ID. | string | `""` | no |
| insufficient\_data\_actions | The list of actions to execute when this alarm transitions into an INSUFFICIENT\_DATA state from any other state. | list | `<list>` | no |
| label\_order | Label order, e.g. `name`,`application`. | list | `<list>` | no |
| managedby | ManagedBy, eg 'CloudDrove' or 'AnmolNagpal'. | string | `"anmol@clouddrove.com"` | no |
| metric\_name | The name for the alarm's associated metric. | string | `"CPUUtilization"` | no |
| name | Name  \(e.g. `app` or `cluster`\). | string | `""` | no |
| namespace | The namespace for the alarm's associated metric. | string | `"AWS/EC2"` | no |
| ok\_actions | The list of actions to execute when this alarm transitions into an OK state from any other state. | list | `<list>` | no |
| period | The period in seconds over which the specified statistic is applied. | number | `"120"` | no |
| statistic | The statistic to apply to the alarm's associated metric. | string | `"Average"` | no |
| threshold | The value against which the specified statistic is compared. | number | `"40"` | no |

## Outputs

| Name | Description |
|------|-------------|
| arn | The ARN of the cloudwatch metric alarm. |
| id | The ID of the health check. |
| tags | A mapping of tags to assign to the resource. |




## Testing
In this module testing is performed with [terratest](https://github.com/gruntwork-io/terratest) and it creates a small piece of infrastructure, matches the output like ARN, ID and Tags name etc and destroy infrastructure in your AWS account. This testing is written in GO, so you need a [GO environment](https://golang.org/doc/install) in your system.

You need to run the following command in the testing folder:
```hcl
  go test -run Test
```



## Feedback
If you come accross a bug or have any feedback, please log it in our [issue tracker](https://github.com/clouddrove/terraform-aws-cloudwatch-alarms/issues), or feel free to drop us an email at [hello@clouddrove.com](mailto:hello@clouddrove.com).

If you have found it worth your time, go ahead and give us a ★ on [our GitHub](https://github.com/clouddrove/terraform-aws-cloudwatch-alarms)!

## About us

At [CloudDrove][website], we offer expert guidance, implementation support and services to help organisations accelerate their journey to the cloud. Our services include docker and container orchestration, cloud migration and adoption, infrastructure automation, application modernisation and remediation, and performance engineering.

<p align="center">We are <b> The Cloud Experts!</b></p>
<hr />
<p align="center">We ❤️  <a href="https://github.com/clouddrove">Open Source</a> and you can check out <a href="https://github.com/clouddrove">our other modules</a> to get help with your new Cloud ideas.</p>

  [website]: https://clouddrove.com
  [github]: https://github.com/clouddrove
  [linkedin]: https://cpco.io/linkedin
  [twitter]: https://twitter.com/clouddrove/
  [email]: https://clouddrove.com/contact-us.html
  [terraform_modules]: https://github.com/clouddrove?utf8=%E2%9C%93&q=terraform-&type=&language=
