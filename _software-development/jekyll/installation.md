---
layout: default
title: Installation
parent: Jekyll
nav_order: 1
---

# Installation

Jekyll
{: .label .label-blue }

Tutorial
{: .label .label-yellow }

@see [Jekyll installation guide](https://jekyllrb.com/docs/installation/)

## Step 1: Install Ruby

Run the following command to check what Ruby version is installed on the system:

```bash
ruby -v
```

On a Debian based Linux distribution run the following command to install ruby using the **apt** package manager:

```bash
sudo apt-get install ruby-full
```

Alternatively to use the **snap** package manager run the following command:

```bash
sudo snap install ruby --classic
```

## Step 2: Install Jekyll

Run the following command to install the jekyll gem:

```bash
gem install bundler jekyll
```

## Step 3: Create a new site

To create a new project named "my-project-name" run the following command:

```bash
jekyll new my-project-name
```

## Step 4: Test that everything works fine

To test that the new site works fine cd into the root directory of your project and run the following command:

```bash
bundle exec jekyll serve
```

Or if you are going to make several changes to the site you might want to use this command:

```bash
bundle exec jekyll serve --livereload
```

The site will be available at `http://localhost:4000`.
