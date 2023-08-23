---
layout: default
title: Collections
parent: Jekyll
nav_order: 3
---

# Collections

Jekyll
{: .label .label-blue }

Reference Manual
{: .label .label-yellow }

@see [Jekyll collections documentation](https://jekyllrb.com/docs/collections/)

Collections are a great way of grouping related content. The y must be defined in the `_config.yml` file as in the following example:

```yaml
# Define Jekyll collections
collections:
  software-development:
    name: Software Development
    permalink: "/:collection/:path/"
    output: true
  system-administration:
    name: System Administration
    permalink: "/:collection/:path/"
    output: true
  drafts:
    output: false
```

In the previous example `name` is a custom optional property that contains a human readable name for the collection. The property `permalink` establishes the format of the url for the pages in the collection. Finally, the `output` property states wether the collection will be outputted in the site or not.
