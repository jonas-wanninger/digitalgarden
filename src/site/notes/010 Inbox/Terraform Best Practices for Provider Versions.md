---
{"dg-publish":true,"permalink":"/010-inbox/terraform-best-practices-for-provider-versions/","tags":["topic/terraform, type/best-practice"],"noteIcon":""}
---


# Terraform Best Practices for Provider Versions

## Declare minimum version in sub-modules

Use the `>=`to specify minimum provider version in each module. This ensures that users don't run into the situation where certain resources are not supported by terraform. Avoids runtime errors.

```
terraform {
  required_providers {
    mycloud = {
      source  = "hashicorp/aws"
      version = ">= 1.0"
    }
  }
}
```

## Declare maximum version in root module

- Applies to [[010 Inbox/Terraform root module\|Terraform root module]]
    - use the `~>` to  allow minor upgrades (right most component)
    - You wan't to upgrade major versions manually

```
terraform {
  required_providers {
    mycloud = {
      source  = "hashicorp/aws"
      version = "~> 1.0.4"
    }
  }
}
```

## Don't enforce maximum version anywhere else

For sub-modules do not enforce the maximum version number. Let the root module decide how to handle this. 

## Don't use the `provider` block in sub-modules 

Specifying the `required_providers` is necessary but don't configure them in your submodule (e.g `provider` block). Let the user of the module decide how to configure the provider. In most instances the provider is inherited automatically from the root module.

```
terraform {
  required_providers {
    mycloud = {
      source  = "hashicorp/aws"
      version = "~> 1.0.4"
    }
  }
}

provider mycloud {
  # dont do this. 
  # Always let the user of the module configure the provider
}
```

## Related

- [[Terraform Best Practices\|Terraform Best Practices]]
- source: [Provider Requirements - Configuration Language](https://developer.hashicorp.com/terraform/language/providers/requirements#best-practices-for-provider-versions)