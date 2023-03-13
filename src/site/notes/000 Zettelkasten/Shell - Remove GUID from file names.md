---
{"dg-publish":true,"permalink":"/000-zettelkasten/shell-remove-guid-from-file-names/","tags":["type/cli-snippet"],"noteIcon":""}
---


# Remove GUID From File Names

```shell
for name in *.md; do
    # remove everything after the last '-' including the dash
    # and add the '.md' extension back
    newname="${name%-*}.md"
    echo mv "$name" "$newname"
done
```