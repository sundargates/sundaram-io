---
title: About Me
date: 2024-08-21
menu:
    main:
        title: About Me
        name: About Me
        weight: 10
---

[//]: # (# About Me)

<!-- I'm happy to talk about work engagements for Q4 2024 and beyond!

[Reach out via email](mailto:jan@janraasch.com) 📧 or [book a zoom call](https://calendly.com/jan-raasch/office-hours) ☎️ -->

## Outline

* [Intro](#intro)
* [Work Experience](#work-experience)
  * [Netflix](#netflix)
    * [Mantis](#mantis)
    * [Flink](#flink)
  * [Uber](#uber)
* [Publications](#publications)
* [Education](#education)
  * [Stanford](#stanford)
* [Talks](#talks)
<!-- * `TODO: add »testimontials«` -->
<!-- * [Skills - How / Process](#how--process) -->
<!-- * [Skills - What / Tech-Stack](#what--tech-stack) -->
<!-- * `TODO: add »past projects« / »portfolio«` -->
<!-- * [Guiding Principles / Focus](#guiding-principles--focus) -->

---

## Intro

My name is Sundaram Ananthanarayanan, and I am a Staff Software Engineer with a decade of experience at various large tech companies. 
Over the years, I have honed my software skills and built distributed systems to tackle problems of various scales.

Over time, my focus has shifted from honing technical skills to understanding the following key questions:

- **What problem are we trying to solve?**
- **Who are we solving this problem for?**
- **What is the likelihood that users will utilize the solution we build?**
- **Is the problem significant enough to incentivize users to collaborate with us on the solution?**

This evolution reflects my transition from solely providing technical expertise to ensuring that we develop solutions that address genuine user needs.

<!-- `# TODO: This should be turned into a proper »services«-section.`

In recent years my focus is on leading by example and making software for product value.

* Do you have a product (in mind or otherwise)?
* Do you want to build an early prototype?
* Or, are you ready to build a functioning MVP?
* Or, do you already have a working product and want to scale up your team with my experience working remotely and with a focus on product thinking and getting your ideas to market faster?

If so, please read on to learn more, or [shoot me an e-mail](mailto:jan@janraasch.com) and let's talk :) -->

<!-- ## Skills

### How / Process

* Focus on the product value proposition.
* Release early. Release often.
* Design software for proven use cases or to prove a use case.
* Prefer asynchronous communication.
* Use synchronous when needed. Then, really make the most out of the time spent together.
* Remote work/team. I have been working remotely for over 6yrs.

### What / Tech-Stack

I have a strong preference for _functional_ programming.

In recent years that has manifested itself in using TypeScript a lot. TypeScript works well with ReactJS and GraphQL, too. Sprinkle in some Go code for serverless APIs, then this is the kind of tech-stack with which I can feel at home.

This tech-stack enables me to deliver on bleeding edge web software, which can easily be shipped natively on iOS, Android, Windows, Mac OS, and Linux via application shells like Electron if needed.

I also have a couple of years of experience with Ruby on Rails applications.

When we are building an early prototype or MVP, I advise keeping it _as low-tech as possible_ and rather use existing APIs and services to get focus on the problem at hand, rather than reinventing the wheel.

Like anybody, I like to keep up-2-date and play around with the new kids on the block. Elixir & Phoenix look very promising. My dear colleague [Alex][alex-url] keeps getting into [rhapsodies about the Live Views][alex-live-views-tweet-url], so I am eager to get my hands dirty with that. Lastly, I have yet to build a larger portion of software with a (pure?) language like Haskell or Elm (which I hear great things about from my friend [Johannes][johannes-url]).

So there's room to grow, but let's not get carried away: I build software for products first, fun tech-stacks second, or third, or `x^th, where x > 3`...

## Guiding Principles / Focus

To sum this up we arrive at the following three guiding principles and one very important question.

❞ **Stay open(-minded)!**

❞ **Product first, software second / if / when / however necessary!**

❞ **Lead by example!**

❞ **What's the product value proposition?** -->

--- 

## Work Experience

### Netflix

**Staff Software Engineer, Data Platform**

_December 2019 - Present_

Broadly, I have been been focusing on making it super easy for engineers at Netflix to publish, transform, and read real-time data. 
The engines and abstractions I have been involved with is used to power a variety of real-time use-cases at Netflix from powering Netflix's famous recommendations to powering shadow canaries for improving the resilience of services at Netflix. 
Below are a set of selected projects I have been lucky to be part of at Netflix.

#### Mantis {#mantis}

Mantis is a stream processing engine coupled with a data transport, similar to Kafka. 
It is uniquely positioned to handle operational data by prioritizing latency over consistency, making it ideal for large software companies like Netflix. 
Originally developed in-house, Mantis is now being used in other companies, including Stripe.

**Migrating Mantis to Kubernetes**

When Mantis was initially built, Apache Mesos was the prevalent DC/OS. Consequently, Mantis was designed around Mesos. However, with the widespread adoption of Kubernetes, Mesos has lost its relevance in the DC/OS landscape and has been deprecated. Even at Netflix, we have migrated away from Mesos to a specialized version of Kubernetes known internally as Titus.

To adapt to this shift, I spearheaded a project to migrate Mantis from Mesos to Kubernetes. This migration posed several unique challenges:

- **Startup Times:** Mantis required startup times on the order of seconds, while Titus at Netflix could only guarantee minute-level latencies.
- **Scale:** The Mantis deployment at Netflix was substantial, with over **60,000** jobs launching on Mesos daily. We needed to migrate these jobs with minimal user disruption.
- **Cost:** Due to the large deployment, Mantis incurred significant compute costs. Our goal was to carry out the migration without increasing the overall cost.

After a couple of years of hard work and leading a team of senior engineers at Netflix, we succeeded in fully transitioning Mantis from Mesos to Kubernetes. This was one of the most challenging projects I've been part of, offering deep insights into building, maintaining, and migrating large distributed systems. In the end, we even leveraged machine learning to significantly reduce costs associated with the project.

#### Flink {#flink}

Flink is a highly popular open-source stream processing engine. 
Unlike Mantis, which prioritizes latency over consistency, Flink focuses on analytical use cases where consistency and correctness are paramount. 
At Netflix, the footprint of Flink is as substantial as that of Mantis and continues to grow rapidly. 
I have been actively involved with various initiatives within the Flink platform at Netflix.

### Backfilling Flink Pipelines using Apache Iceberg

One of the major pain points for teams building Flink pipelines is the need to maintain separate batch jobs that pull data from a data warehouse during outages. This approach has several limitations:

- **Separate Batch Pipeline:** Teams must build a separate batch pipeline using Spark DSL, which differs significantly from Flink's DSL.
- **Out-of-Date Pipelines:** Batch pipelines can easily become outdated, rendering them useless when they are actually needed.
- **High Costs:** Backfilling based on historical data using the Flink pipeline itself incurs exorbitant costs, as Kafka storage is significantly more expensive compared to data warehouses that use cost-effective object storage.

To address these issues, I developed a new system that allows users to backfill their Flink pipelines using a streaming Iceberg source. 
This source mimics the properties of Kafka, providing the same ordering guarantees without the high storage costs associated with Kafka. 
This project has been highly successful at Netflix, with hundreds of Flink jobs adopting this solution to backfill their pipelines in the event of an outage. 
Additionally, I helped open-source the project, and it is now being used by other organizations that utilize both Flink and Apache Iceberg.


<!-- I work with my clients to bring their ideas to market.

Whether you are a small/young start-up or a business unit of a larger already running company we will focus on what your product value proposition is, and how we can test our assumptions about this as early and light-weight as possible.

I have built early prototypes for my client founders to showcase their ideas to possible clients & investors.

For my bigger clients, I supported their existing teams to meet their milestones. In these kinds of scenarios, my focus is on leading by example and thus sharing my experience about how to build scalable software on the web, how to work in a remote set-up, and how to communicate efficiently with the whole team.

Interested? [Let's talk business!](mailto:jan@janraasch.com) -->

### [Uber](https://www.uber.com) {#uber}

**Senior Software Engineer II, Developer Infrastructure**

_June 2016 - December 2019_

#### Submit Queue

1000s of engineers committing changes concurrently to a repository leads to frequent master breakages. 
Explored & conceived a new system called SubmitQueue that guarantees an always-green master at scale. 
At Uber, SubmitQueue handles 1000s of commits/hr submitted by 1000s of engineers every day.

### [Baidu Silicon Valley AI Research Lab](http://research.baidu.com/)

_Jan 2016 - June 2016_

<!-- _»t for translation. Professional translations into any world language.«_ -->

**Role:** Software Engineer.

<!-- At tolingo I had the opportunity to grow from a Frontend / JavaScript engineer to a full-fledged Full Stack Developer.

We were a small team of 2-3 engineers working on the internal software stack and the customer-facing web-shop.

I worked very closely with our stakeholders to enable the team of sales agents, translation project managers, and translators to deliver high-quality results efficiently through our custom-built software solutions. -->

### [Twitter](https://x.com/)

_June 2014 - Jan 2016_

**Role:** Software Engineer.

**Teams:** Growth Infrastructure, Engineering Effectiveness.

ePages was my first professional engagement in the world of web software. I was eager to get out of the theoretical world of pure mathematics academia and I succeeded in picking up the tools and practices of web development very fast thanks to my strong basis in rational problem-solving.

We moved the existing frontend stack to the leading frontend stack of the time. Also, I was part of a spear-heading team that led the way to an all-new version of the software while implementing agile practices into the work-flow.

---

## Publications

I have been fortunate to publish some of the work I conducted during my time at Stanford and at various companies where I have been employed.
For a complete list of my publications, please refer to my [Google Scholar profile](https://scholar.google.com/citations?user=R_MUwMwAAAAJ&hl=en).

1. [**Keeping Master Green at Scale**](https://dl.acm.org/doi/10.1145/3302424.3303970) <br>
   [EuroSys '19, Dresden, Germany](https://2019.eurosys.org/) 

2. [**Deep Speech 2 : End-to-End Speech Recognition in English and Mandarin**](https://dl.acm.org/doi/10.5555/3045390.3045410) <br>
   [ICML '16, New York, NY, USA](https://icml.cc/Conferences/2016)

3. [**Reliable Computing with Ultra-Reduced Instruction Set Coprocessors**](https://ieeexplore.ieee.org/document/6241581) <br>
   [DAC '12, San Francisco, CA, USA](https://www.dac.com/)

4. [**Low cost permanent fault detection using ultra-reduced instruction set co-processors**](https://doi.org/10.7873/DATE.2013.196) <br>
   [DATE '13, Grenoble, France](https://www.date-conference.com/)


## Education

### [Stanford University](https://www.stanford.edu/) {#stanford}

_September 2012 - June 2014_

_Master of Science in Electrical Engineering - Distributed Systems_

### [College of Engineering, Guindy](https://ceg.annauniv.edu/)

_Graduated in June 2012_

_Bachelors in Information Technology_

---

## Talks

1. **Mantis: Stream Processing for Operational Data** <br>
   [Data Engineering Things](https://dataengineerthings.substack.com/p/data-engineer-things-newsletter-11), [Slides](/slides/det.pdf)

2. **Backfill Streaming Data Pipelines in Kappa Architecture** <br>
   [DATA+AI Summit '22](https://databricks.com/dataaisummit/north-america), [Video](https://youtu.be/aCIWI5k7deM?si=UOllcVPiLRL2A9Oz), [Slides](/slides/dais22.pdf)

2. **Backfill Flink Pipelines with Apache Iceberg** <br>
   [Flink Forward '21](https://www.flink-forward.org/global-2021), [Video](https://www.youtube.com/watch?v=tB4rx_W9Xqw), [Slides](/slides/ff21.pdf)

3. **Keeping Master Green at Scale** <br>
   [EuroSys '19](https://2019.eurosys.org/), [Video](https://vimeo.com/358691692), [Slides](/slides/eurosys19.pdf) 
