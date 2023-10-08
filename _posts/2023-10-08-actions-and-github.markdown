---
title:  "Automate Your Blog Posts with GitHub Actions"
subtitle: "Streamlining Your Blogging Workflow"
author: "Wferr"
avatar: "img/authors/wferr.png"
image: "img/b.jpg"
date:   2023-10-08 12:12:12
---

### Introduction

<p style="font-size: 15px;">As a passionate blogger who loves both writing and maintaining a blog on GitHub Pages, you know that managing your blog can be a rewarding yet time-consuming endeavor. The good news is that you can streamline your blogging workflow and save precious time through automation using GitHub Actions. In this article, we'll explore how to automate your blog post deployment on GitHub Pages, making your blogging journey smoother and more efficient.</p>

### I. Requirements

Before we dive into automating your blog posts, let's ensure you have the necessary tools and prerequisites in place:

    GitHub Pages Blog: You should already have a blog hosted on GitHub Pages. If you don't, you can set up a GitHub Pages repository to get started.

    Jekyll: If your blog is built with Jekyll, make sure it's properly set up. Jekyll is a popular static site generator that works seamlessly with GitHub Pages.

    Node.js: Node.js is a JavaScript runtime that will allow us to write custom scripts for automation. Ensure you have Node.js installed on your local machine.

    GitHub Actions: Familiarize yourself with GitHub Actions, which is the automation and CI/CD platform provided by GitHub. It enables you to create custom workflows for your repositories.

### Writing a Node.js Script

To automate your blog post deployment, you can create a Node.js script that gets lastest post of your blog. Here's a simple script as an example:

```shell
import fs from 'fs/promises';
import Parser from 'rss-parser';
const parser = new Parser();
 
try {
  const { items } = await parser.parseURL('https://libialany.github.io/feed.xml');
  let updates = `<!-- start latest posts -->\n`;
  for (let i = 0; i < 3; i++) {
    const { link, title } = items[i];
    const row = `- [${title}](${'https://libialany.github.io/'+link.slice(0,-5)})\n`;
    updates = updates.concat(row);
  }
  updates = updates.concat('<!-- end latest posts -->');
  const currentText = await fs.readFile('README.md', 'utf8');
  const postsSection = /<!-- start latest posts -->[\s\S]*<!-- end latest posts -->/g;
  const newText = currentText.replace(postsSection, updates)
  await fs.writeFile('README.md', newText);
} catch (error) {
  console.error('there was an error:', error.message);
}
```
This script builds your Jekyll site, performs optional optimizations, and deploys it to GitHub Pages.

### Writing a Workflow YAML File

To automate the execution of the script whenever you make changes to your blog, you can create a GitHub Actions workflow. Create a .github/workflows/deploy.yml file in your repository with the following content:

```shell
name: Build README

on:
  workflow_dispatch:
  repository_dispatch:
    types: [scrape]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Check out repo
        uses: actions/checkout@v3
      - name: Use Node
        uses: actions/setup-node@v3
        with:
          node-version: "18.x"
      - name: Install node dependencies
        run: npm install
      - name: Check for RSS feed updates
        run: npm run scrape
      - name: Commit and push
        run: |-
        ... more code
```

This YAML file defines a GitHub Actions workflow that runs whenever you push changes to the main branch. It sets up Node.js, installs dependencies, and executes your Node.js script.

### Interesting Applications of GitHub Actions

-Continuous Integration (CI): Automate testing and validation of your blog's code to ensure it's error-free before deployment.

-Scheduled Posts: Use GitHub Actions to schedule and automate the publishing of blog posts at specific times or dates.

-Backup and Recovery: Create automated workflows that back up your blog's content and settings regularly, making it easier to recover from any accidental data loss.

-Notify Subscribers: Automatically send notifications to your subscribers or social media followers whenever you publish a new blog post.

-Security Scans: Use GitHub Actions to scan your blog for security vulnerabilities and receive alerts or automatic fixes for potential issues.

[link to the complete code](https://github.com/libialany/libialany)