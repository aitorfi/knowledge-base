---
layout: default
title: Themes
parent: Jekyll
nav_order: 2
---

# Themes

Jekyll
{: .label .label-blue }

Reference Manual
{: .label .label-yellow }

@see [Jekyll theme marketplace](https://jekyllthemes.io/), [GitHub jekyll-theme topic](https://github.com/topics/jekyll-theme)

The theme of a jekyll site is configured in the file `_config.yml` on the root directory of the project.

```yaml
# Build settings
theme: minima
plugins:
  - jekyll-feed
```

## Remote themes

If instead you want to use a remote theme you can do it using the `remote_theme` directive and adding the `jekyll-remote-theme` plugin:

```yaml
# Build settings
remote_theme: just-the-docs/just-the-docs@v0.5.1
plugins:
  - jekyll-feed
  - jekyll-remote-theme
```

To add the gem `jekyll-remote-theme` as a dependency to your project run the following command:

```bash
bundler add jekyll-remote-theme
```
