---
title: About Me
date: 2024-08-21
menu:
    main:
        title: About Me
        name: About Me
        weight: 10
---

## Outline

* [Intro](#intro)
* [Work Experience](#work-experience)
  * [Netflix](#netflix)
    * [Mantis](#mantis)
    * [Flink](#flink)
  * [Uber](#uber)
    * [Submit Queue](#submitqueue)
  * [Baidu Research Lab](#baidu)
  * [Twitter](#twitter)
* [Side Projects](#side-projects)
  * [BigBeans](#bigbeans)
* [Education](#education)
  * [Stanford](#stanford)
* [Publications](#publications)
* [Talks](#talks)
<!-- * `TODO: add »testimontials«` -->
<!-- * [Skills - How / Process](#how--process) -->
<!-- * [Skills - What / Tech-Stack](#what--tech-stack) -->
<!-- * `TODO: add »past projects« / »portfolio«` -->
<!-- * [Guiding Principles / Focus](#guiding-principles--focus) -->

---

## Intro

I am a Staff Software Engineer with a decade of experience at various large tech companies. 
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

{{< experience netflix Netflix "December 2019 - Present" "Staff Software Engineer, Data Platform" >}}

Broadly, I have been been focusing on making it super easy for engineers at Netflix to publish, transform, and read real-time data. 
The engines and abstractions I have been involved with is used to power a variety of real-time use-cases at Netflix from powering Netflix's famous recommendations to powering shadow canaries for improving the resilience of services at Netflix. 
Below are a set of selected projects I have been lucky to be part of at Netflix.

#### [Mantis](https://netflix.github.io/mantis/#why-we-built-mantis) {#mantis}

Mantis is a stream processing engine combined with a data transport system, akin to Kafka and Flink. 
At its core, Mantis is engineered to handle large volumes of **operational data** with minimal latency. 
It achieves this by leveraging two essential properties of operational data:

- **Needle in a haystack**: Most operational data is noise (think of all the logs, metrics, and events your service generates), making it unnecessary to publish every bit of it.
- **Diminishing value over time**: The usefulness of operational data rapidly decreases with time, making real-time processing crucial. For instance, if you need to autoscale a service based on specific metrics, data that is 10 minutes old is practically useless. In other words, the value of the data diminishes quickly over time.

Mantis capitalizes on these properties by providing a transport system that performs:

- **Edge-level filtering and transformations**: Mantis filters out the noise and processes only the valuable data at the edge layer. Data that has subscribers is considered **valuable**.
- **Send, Don't store**: Mantis avoids storing data, instead sending it directly from the edge to the processing layer in real-time. This approach exploits the diminishing value of operational data, ensuring that only the most recent data is processed.

In my opinion, Mantis is uniquely suited for addressing challenges in the operational domain, making it an excellent fit for large software companies like Netflix. 
Originally developed in-house, Mantis is now also being utilized by other companies, including Stripe.

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

{{< experience uber Uber "May 2016 - December 2019" "Senior Software Engineer II, Developer Infrastructure" >}}

#### Submit Queue {#submitqueue}

At Uber, we managed a monorepo that thousands of engineers were committing changes to concurrently. 
Monorepos offer significant advantages, such as improved code sharing, consistent tooling, and streamlined platform updates. 
However, a major downside is that the master branch frequently breaks due to the high volume of commits. 
This was a significant issue at Uber, where the master branch was broken 50% of the time.

To resolve this problem, I led a team to develop a system called Submit Queue. 
The primary goal of Submit Queue is to ensure that the master branch remains stable. 
It achieves this by running all necessary checks on changes before merging them into the master branch. 
The simplest approach would be to queue the changes and run checks sequentially, but this would be inefficient and not scalable.

We identified two critical requirements for the system:
1. **Scalability**: The system needed to handle thousands of commits per day.
2. **Low Latency**: Engineers at Uber are highly sensitive to the time it takes for their changes to be merged.

To meet these challenges, we developed two innovative techniques:
1. **Probabilistic Speculation**: This technique involves speculating on the outcome of checks before they are run, allowing us to perform checks in parallel and reduce overall latency. We utilized machine learning models to predict the outcomes.
2. **Conflict Analysis**: By analyzing the build graph, we could detect conflicts between changes. This enabled us to run checks for changes affecting independent parts of the system in parallel.

The implementation of Submit Queue was a tremendous success, reducing the master branch breakage rate from 50% to 0%.

You can read more about this system in the [paper][submitqueue-paper] we published at EuroSys '19.

{{< experience baidu "Baidu Silicon Valley AI Research Lab" "Jan 2016 - May 2016" "Software Engineer, Speech Inference" >}}

At Baidu, I contributed to the Deep Speech 2 project, which aimed to develop a highly accurate speech recognition system capable of transcribing both English and Mandarin speech using Deep Learning. 
My primary responsibility was to design and implement the inference APIs and backend infrastructure, enabling developers to seamlessly integrate the speech recognition system into their applications.

{{< experience twitter "Twitter" "June 2014 - Jan 2016" "Software Engineer in Growth Infrastructure & Engineering Effectiveness" >}}

Twitter was my first job after graduating from Stanford. 
I initially joined the Growth Infrastructure team, where I worked on various projects, including the development of a system to store and retrieve users' address book contacts. 
This system played a crucial role in suggesting people for users to follow on Twitter based on their existing contacts.

It was incredibly fascinating to see Scala in action at Twitter. 
I gained significant insights into functional programming and deepened my understanding of concepts such as monoids, monads, and functors.

---

## Side Projects {#side-projects}

### [BigBeans](https://www.bigbeans.ai) {#bigbeans}

BigBeans is a project I started with a few friends to help engineers and data engineers learn ML by practicing on well-known datasets. 
We offer a set of curated problems designed to teach ML concepts and their practical applications.

Unlike platforms such as Kaggle, BigBeans emphasizes learning rather than competition. 
Each problem on BigBeans has a specific threshold of correctness that must be met for the solution to be accepted. 
These thresholds are tailored to the techniques being taught in each problem.

For example, we feature three versions of the MNIST dataset on BigBeans, each with a different 
threshold of correctness and a unique technique required to solve it. 
This approach ensures that users who know a particular technique, such as Support Vector Machines (SVM), 
can practice problems specifically designed for that technique and receive validation that they are 
applying it correctly.

---

## Education

### [Stanford University](https://www.stanford.edu/) {#stanford}

_September 2012 - June 2014_

_Master of Science in Electrical Engineering - Distributed Systems_

### [College of Engineering, Guindy](https://ceg.annauniv.edu/)

_Graduated in June 2012_

_Bachelors in Information Technology_

---

## Publications {#publications}

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

[submitqueue-paper]: #publications
