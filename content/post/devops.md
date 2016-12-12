+++
categories = ["DevOps"]
description = ""
tags = ["aws", "grafana"]
date = "2016-12-12T20:37:04+02:00"
title = "The beauty of DevOps"
+++

<img src="https://s3.eu-central-1.amazonaws.com/gruberb-blog/scrum.jpg" />

For my latest client, I got hired as a Fullstack JavaScript developer, plus DevOps, plus Frontend. The project is to rebuild the old PHP codebase onto a new stack containing Node, Angular and Microservices. The deployment is done via Docker and DockerCloud, hosted partly on AWS servers. As complicated as it sounds, new projects don't have the nitty gritty problems legacy systems have. I think what you have to bring to such a project is a broad understanding of each technology and how they interact together.  

My previous position was as a Senior Frontend Developer, working with Angular 1 and 2. There, you have to have a deep understanding of the framework, and how to get the latest percentages of performance out. As well as how to constantly refactor an ever growing codebase. So sometimes people think that to setup the whole stack, they have to have a really deep understanding of every technology. But sometimes, it's just not needed. You can set up a MongoDB database for a certain microservice, just knowing this form of database works fine. Later on, you can hire a Mongo specialist or look deeper into how to scale and improve performance with this technology.

This gives you a lot of freedom, but also responsibility. What I deal with at the moment, are the so called "DevOps". Since my last project was implementing NodeJS patterns and structure, I sort of feel the beauty of the pure analytical work of setting up and monitoring services. There is no big guessing or "let's see" factor. It's different approach then pure programming. Finally, you have to have a clear picture of which service should talk to which, how they should give feedback and how and with which tools you measure performance.  

Again, all the little details can be nasty and hard, but for the first few days after this shift in perspective, you have the feeling of power and overview of the system. In return, it helps to understand when a service should respond with critical feedback, and what this feedback should look like. Sometimes, Sometimes I think, starting from this perspective can help decide which service should contain which logic, and how big a certain microservice should get.

As a front end developer, I appreciate starting the project with a clear UX/UI guideline and idea. From a backend developer perspective, I now appreciate the DevOps-First perspective. Once you know how the system should respond in different situations, than you know you how to structure your codebase.

Implementing a monitoring microservice, which receives important messages from other services, sends them to an InfluxDB, and Grafana takes this data to display the current affairs. Seeing how well and nicely this all plays out gives every developer a warm heart. What more can you ask for just before Christmas?
