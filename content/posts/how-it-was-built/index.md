---
title: "How this website was built"
date: 2020-12-04T06:54:35+01:00
author: Diego
draft: false
ShowToc: true
Tags: 
    - Hugo
    - Terraform
    - Blog
categories: 
    - Blog
---

In this first post I want to summarize how and why I created this website, some technical and personal requirements that draw my decisions.
Most of this is highly opinionated so feel free to disagree and to point out any mistakes.
Throughout this write up I will link to the resources on my Github page as: 

1. "Talk is cheap. Show me the code." - Linus Torvalds 
2. I do not want to have to update this page each time I make a small change to something.

Moreover, there are a million guides out there on how to set up the various tools that I used. I will not go into tutorial level of details here but I will point out the gotchas that costed me quite a lot of time to figure out.
# Requirements

While thinking how to build this I have these basic ideas into my mind

1. Time is finite, work smart not hard
2. I am not a frontend person
3. Minimal maintenance
4. No cookies, no tracking, no analytics. I do not want to deal with GDPR, etc.
5. I want to improve my technical skills while doing this. In particular about AWS/terraform
6. Based on open source stack as much as possible
7. As cheap as possible

From these considerations I came up with the following list of requirements
   
   * Static website
   * Serverless
   * It should be automatically build from commits to Github
   * The infrastructure should be defined via terraform
   * No logs or cookies whatsoever

Combining all these reasons and after some googling I decided to go for a website built with [Hugo](https://gohugo.io) deployed in a private S3 bucket with CloudFront distributing the content. 

# Basic workflow

The workflow that I use for publishing content is the following

    Markdown -> Github -> Github action builds hugo -> S3 -> CloudFront

in particular the Github action is enabled for each commit/merge into master. Which allows me to work on drafts and experiments locally without impacting the website or triggering any cache invalidation. The full Github action is accessible [here](https://github.com/dfioravanti/blog/blob/master/.github/workflows/deploy.yml).

This workflow was built using this three resources:
* [Hugo actions](https://github.com/peaceiris/actions-hugo): community maintained github actions used to interact with hugo.  
* [Hugo hosting and deployment](https://gohugo.io/hosting-and-deployment/hosting-on-github/): explains how to publish a Hugo website to github. It can be adapted into publishing to S3.
* [AWS github actions](https://github.com/aws-actions/configure-aws-credentials): the official AWS way to interact with your AWS account in a github action workflow.

# Code

The code for this blog and the infrastructure behind it is hosted on my github
* [blog](https://github.com/dfioravanti/blog)
* [infrastructure](https://github.com/dfioravanti/terraform)

# Development

Developing this website was relatively straight forward. Both Hugo and terraform have excellent tutorials out there. I used the following resources

* [Hugo own tutorial](https://gohugo.io/getting-started/quick-start/): easy and clear tutorial to understand the very basic of Hugo
* [Hugo and AWS](https://lustforge.com/2016/02/27/hosting-hugo-on-aws/): it is a bit out of date but it put me on the right direction
* [Hugo and CloudFront](https://monkeypatch.ca/hugo_s3/): a much more recent resource about deploying Hugo on AWS
* [Hugo and Lambda@edge](https://simpleit.rocks/golang/hugo/deploying-a-hugo-website-to-aws-the-right-way/): where I got the idea of how to use lambda@edge to redirect `example.com/hello/` to `example.com/hello/index.html`
* [Terraform up and running](https://www.terraformupandrunning.com/): simply the best resource out there to learn terraform

## Gotchas that made me lose time

Despite all the good resources that I used I bumped into some problems. Most of them are idiosyncrasies of AWS and we just need to live with them
### Both certificate and certificate validator have to be in the us-east-1 zone

If you want to use a HTTPS certificate managed by AWS in CloudFront then you need to have both the `aws_acm_certificate` and the  `aws_acm_certificate_validation` terraform resources in the `us-east-1` zone. The fact that you need the certificate into `us-east-1` is written everywhere meanwhile the fact that the certificate validator has to be there too is only hinted here and there. This is a hard requirement, the validation will fail otherwise.

### By default cloudfront does not inherit the S3 404 page you need to set it up yourself.
  
When you deploy a static website in S3 you need to set up both an index and an error page. CloudFront ignores both of them. If you want the same behavior in CloudFront you need to specify both pages into you CloudFront distribution.

### The lambda for lambda@edge must be in us-east-1

To be fair this is written everywhere but I still missed it. You can deploy a lambda in any region but if you want to use it as a lambda@edge you need to deploy it in the `us-east-1` region otherwise it will not work.
### Logging with lambda at edge is a mess. 

I ended up dropping logging as I do not want to deal with GDPR by even having the chance of recording an IP address or any other sensitive data. But before taking this decision I briefly looked into how to log errors/outputs from a lambda@edge function. [This official AWS](https://aws.amazon.com/blogs/networking-and-content-delivery/aggregating-lambdaedge-logs/) page gives an idea of the complexity of the matter. [This](https://www.reddit.com/r/aws/comments/9viur4/centralized_logging_for_lambda_edge/) reddit thread seams to indicate that there is a better way to do it but I did not look into deep enough to come with a strong opinion.
