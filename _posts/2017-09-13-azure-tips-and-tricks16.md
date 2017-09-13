---
layout: post
title: "Azure Tips and Tricks Part 16 - Deploy Jekyll Site Hosted on GitHub to Azure"
excerpt: "Learn how to quickly deploy a Jekyll based site hosted on GitHub to Azure"
tags: [azure, windows, portal, cloud, developers, tipsandtricks]
share: true
comments: true
---

## Intro

Most folks aren't aware of how powerful the [Azure](http://www.azure.com) platform really is. As I've been presenting topics on Azure, I've had many people say, "How did you do that?" So I'll be documenting my tips and tricks for Azure in these posts.

## The Complete List

[Click here to view the complete list of Azure Tips and Tricks ](https://michaelcrump.net/azure-tips-and-tricks-complete-list/)

## Deploy Jekyll Site Hosted on GitHub to Azure

If you have already have an existing [Jekyll](https://jekyllrb.com/) based site that is hosted on GitHub, you can easily deploy that site to [Azure App Services](https://azure.microsoft.com/en-us/services/app-service/web/). 

But why? If [GitHub Pages](https://pages.github.com/) is free, then why pay?

* You might want to push your site to a private repo (instead of public)
* Setting up "real" SSL, compared to the [workarounds](https://css-tricks.com/switching-site-https-shoestring-budget/) (see comments)
* Taking advantage of [deployment slots](https://docs.microsoft.com/en-us/azure/app-service-web/web-sites-staged-publishing). 

I'm sure there are more, but those are top of mind for me. 

## Let's begin

I'm assuming you already have a GitHub Pages site that uses Jekyll hosted on GitHub. If that is true, then the first thing that you'll want to do is grab these three files. 

* [deploy.cmd](https://github.com/mbcrump/mbcrump.github.io/blob/master/deploy.cmd) - is a [Kudu](https://github.com/projectkudu/kudu) Deployment script that handles setup and deployment of the web site and ensures Ruby is installed
* [getruby.cmd](https://github.com/mbcrump/mbcrump.github.io/blob/master/getruby.cmd) - is a site that ensure the latest version of Ruby is installed and ensures Jekyll has been built
* [.deployment](https://github.com/mbcrump/mbcrump.github.io/blob/master/.deployment) - is a configuration file  that Kudu understands that calls the `deploy.cmd` script
* [Gemfile](https://github.com/mbcrump/mbcrump.github.io/blob/master/Gemfile) - you probably already have this but ensure it is there and if not then just copy mine. 

***Thanks goes to [Khalid Abuhakmeh](https://github.com/khalidabuhakmeh) for writing the scripts***

Once you have these three files, ensure they are in the root of your public GitHub pages site (ex. something.github.io)

You'll want to go inside of your **Azure Portal** (or use the CLI tools) and create an **App Service** -> **Web App**. Once the site is deployed, then go to **Deployment Options** and select GitHub, your project and press OK. 

<img style="border:3px solid #021a40" src="https://michaelcrump.net/files/azuretip16.gif">

You should see "Settup up Deployment Source..." in the notification windows. You'll probably want to wait a good 15 to 20 minutes for Azure to setup everything. You can stay on the **Deployment Options** blade and you should finally see a green check mark that it completed successfully. Now you can navigate to the URL listed on the **Overview** blade. 


## Want more Azure Tips and Tricks?

If you'd like to learn more Azure Tips and Tricks, then follow me on [twitter](http://twitter.com/mbcrump) or stay tuned to this blog! I'd also love to hear your tips and tricks for working in Azure, just leave a comment below. 