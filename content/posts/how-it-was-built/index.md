---
title: "How this website was built"
date: 2020-11-26T06:54:35+01:00
draft: true
keywords: 
    - test
    - lol
---

# Requirements

While thinking how to build this I have these basic ideas into my mind

1. Time is finite.
1. I am not a frontend person. There is no competitive advantage for me in building a website from scratch.
2. Minimal maintenance.
3. I want to improve my technical skills while doing this. In particular about AWS/terraform.
4. Based on open source stack as much as possible.

From these consideration I came up with the following list of requirements
   
   * Static website
   * Serverless
   * It should be automatically build from commits to Github
   * It should use let's encrypt

Combining all these reasons and after some googling I decided to go for [Hugo](https://gohugo.io) deployed on a S3 bucket. 

# Basic workflow

The workflow that I use for publishing content is the following

    Markdown -> Github -> Github action builds hugo -> S3

# Deployment

[This](https://gohugo.io/hosting-and-deployment/hosting-on-github/) explains how to push to github. It can be adapted into building and pushing to S3.

AWS provides [github actions](https://github.com/aws-actions/configure-aws-credentials) to interact with your AWS account