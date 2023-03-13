---
{"dg-publish":true,"permalink":"/000-zettelkasten/terraform-generate-least-privelige-rights-script-for-terraform-execution/","tags":["type/code-snippet, topic/terraform,"],"noteIcon":""}
---


# Execute This

```shell
TF_LOG=trace 
TF_LOG_PATH=plan.log 
terraform plan  

cat plan.log | grep "DEBUG: Request" | cut -d' ' -f 11 | sort | uniq > plan-api-calls.txt
```

## See Also

- [[000 Zettelkasten/Terraform MOC\|Terraform MOC]]