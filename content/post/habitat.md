+++
title = "Deploying Node apps with Habitat"
Description = ""
Tags = ["devops"]
Categories = []
date = "2018-07-10T09:51:55+01:00"
draft = true
+++

Deploying apps within a company and for a bigger project seems more complicated. But, with enough team members and AWS or Google Cloud, deploying apps has never been easier. For my current side project (YNABDoctor), I needed a solution to make my API available in public. Though it was just for my private needs and I didn't plan to let other users register and login to it. Therefore, I looked for solutions.

1. AWS or Google Cloud
The obvious choice was, at first, to use one of the big names. Since I have experience with AWS and Google Cloud, I wanted something fast and easy. So obviously I picked procedures I already knew. Ansible here, a bit of API Gateway there and my app would be on AWS. After a bit of researching and rational thoughts (if there is such a thing), I reminded myself that I:
- Don't need to scale
- Don't need to setup a whole infrastructure
- Don't want to spend much money on it

So I downsized in my mind and went on with the next, obvious choices.

2. Digital Ocean or Heroku
What can possible be wrong with that, right? Digital Ocean and Heroku make it so easy to deploy Node apps, it's almost scary. The tutorials especially on Digital Ocean are the best ones out there and their UI is so slick and easy to use, it's hard not to choose them, even if it comes with an additional cost. Digital Ocean costs at least 5 Dollar a month, whereas Heroku is free (in the basic version). You have to wait a few seconds because the container is shutting down after not being used (the 'free' in free has to come from somewhere, right?) but that's not a problem at all for me. I just want to use the API and my own created apps for it (mobile and web) on the go. I can wait a few seconds every once in a while.

But then it came to my mind that I already rented a server, in France - with Kimsufi, and already pay 10 Euros a month for it. So I thought: Hey, lets use that for the beginning. And here I went.

3. Kimsufi server
I ssh'd into my server and looked around. There was almost nothing I needed to make the node app running. For the first time in a long long time it came to my mind why are those provisioning and build tools are out there. Because it's not really magic: You get a basic Linux Distro which talks to the hardware and offers a few UNIX tools to get by. Everything else is on you (and millions of developers who create tools for those scenarios).

A while back I had a chat with an old work colleague and he talked about Habitat. I didn't really get it at the time, but he seems super excited about it and used it already in production at the StartUp we are used to work at together. I rememberd the linkt he sent me and off I went on my Journey to deploy my little Node app from "scratch".

### What does habitat do?

