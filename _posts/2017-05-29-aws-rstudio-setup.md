---
title: "Setting up RStudio on Amazon Elastic Cloud Compute (EC2)"
date: "2017-05-29"
tags:
  - data-science
---

I've been trying to use R every day for the last few months to build up my muscles. This has meant running through tutorials and some personal projects, including developing a Shiny app. Faced with the prospect of a few days holiday where I won't have my laptop - but will have my iPad - I decided to get RStudio and Shiny servers running on a remote computer so I could still R through the iPad's browser. This is doubly useful as I haven't used cloud-based service before, so will give me some experience of it.

Googling immediately pointed to AWS [Amazon Web Services](https://aws.amazon.com/) as a solution for RStudio Server through the browser, via the sterling work of [Louis Aslett](http://www.louisaslett.com/RStudio_AMI/). Louis maintains custom Amazon Elastic Cloud Compute [EC2](https://aws.amazon.com/ec2/) instances (virtual computers). These come pre-configured with loads of tools and dependencies: updated Ubuntu, latest R, RStudio and Shiny Servers, Jupyter notebook, Dropbox integration, and others.

The step-by-step video on Louis' website is a little out of date compared to the setup wizard found at present. I referred to a blog post by [Matt Strimas-Mackey](http://strimas.com/r/rstudio-cloud-1/) as it reflected the current EC2 launch steps and explores SSHing (secure access) in more detail.

It took me about 20 minutes to get up an running, including a password reset on RStudio Server adn Dropbox syncing. Here's RStudio on my iPad. 


<figure class="align-centre">
  <a href="/assets/images/data-science/rstudio-ipad.jpg"><img src="/assets/images/data-science/rstudio-ipad.jpg" alt="RStudio running from EC2 in iPad's Safari"></a>
  <figcaption>RStudio running from EC2 in iPad's Safari.</figcaption>
</figure>