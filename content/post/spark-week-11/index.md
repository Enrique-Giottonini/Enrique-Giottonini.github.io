---
title: Encora Spark Week 11. Testing the open-source waters & fundamentals.
date: 2024-07-15
math: true
diagram: true
---

tl;dr: I've been working on getting to know what OSS is about, and how to be part of it by contributing to a project. I've also been working on improving my technical skills, especially in Java and backend web development.

# **Index**

1. [**Insights from trying to contribute to an open-source project**](#insights-from-trying-to-contribute-to-an-open-source-project)
2. [**Possible projects to work on in the next weeks**](#possible-projects-to-work-on-in-the-next-weeks)
3. [**Java Backend Developer track**](#java-backend-developer-track)

# <a id=insights-from-trying-to-contribute-to-an-open-source-project></a>**1. Insights from trying to contribute to an open-source project**

My objective for this week was to get a succesful Pull Request (PR) accepted into an open-source project. I didn't know where to start, and seeing the amount of contributors and contributions in a single project was overwhelming. Good thing that I was kindly provided with a list of readings from the Spark team, which helped me to understand the basics of how to contribute to a project.

I first learned about [why people contribute to open-source projects](https://www.planetcrust.com/why-do-people-contribute-to-open-source-projects/?utm_campaign=blog). If you think about people are sharing their work to be seen by others for **_free_**, and contributors are not actually expected to be payed for their work. The article explains that people contribute to open-source projects for a variety of reasons, including the opportunity to learn new skills, to build a portfolio, to give back to the community, and to work on projects that they find interesting, to promote open-source culture, and to iterate more quickly in the development of a project and fixing errors as more eyes see the code. The last point is what I imagine corporations like Google, Facebook, and Amazon are doing with their open-source projects, while the first points are what I think I can get from contributing to a project.

Now that I have cleared my motivations [how do I contribute to open source?](https://opensource.guide/how-to-contribute/). I gathered some insights from this article and ended up with a list of steps to follow:

1. **Find a project**: I can start by looking for projects that I use and love, or that I think are interesting. I can also look for projects that are looking for contributors, or that have issues labeled as "good first issue" or "help wanted" (e.g. [Good first issue](https://goodfirstissue.dev/), [Open source projects for beginners](https://hackernoon.com/how-to-find-open-source-projects-for-beginners)).
2. **Evaluate the project**:
   - Do I understand the project's goals and how it works?
   - Do I have the skills to contribute to the project?
   - Are issues getting resolved recently?
   - Are PRs getting reviewed and merged?
   - Are there any low-hanging fruits such as typos, documentation, simple bug fixes?
3. **Get the project running locally**: I can follow the project's README to get the project running locally, and to understand how the project is structured.
4. **Follow the contribution guidelines**: I can read the project's contribution guidelines to understand how to contribute to the project, and to understand the project's coding style and conventions.
5. **Find an issue to work on**: I can look for issues labeled as "good first issue" or "help wanted", or I can look for issues that I think I can help with.
6. **Work on the issue**: I can fork the project, create a new branch, make the changes, and create a PR.
7. **Create a PR**: I can create a PR with a clear title and description, and I can link the PR to the issue that I'm working on.
8. **Review the PR**: I can ask for feedback on the PR, and I can make changes based on the feedback.
9. **Get the PR merged**: I can get the PR reviewed and merged, and I can celebrate my contribution!

As for now I'm in step six, I've found an issue that I think I can help with, and I'm working on it, which is basically adding documentation for a specific function in the project. I choose this issue because it was labeled as "good first issue", and because its my first time contributing to an open-source project and I want to start with something simple.

The project I'm contributing to is [Eclipse Collections](https://github.com/eclipse/eclipse-collections), a framework for Java with optimized data structures and a rich, functional and fluent API. I chose this project because I have an idea on how they extend the Java Collections API, and I quite undertood some of the codebase. It's an active repository, and have issues labeled as "good first issue" which means that they are looking for newbie contributors like me.

# <a id=possible-projects-to-work-on-in-the-next-weeks></a>**2. Possible projects to work on in the next weeks**

I would like to work on the Eclipse Collections project but this time fixing a bug. Other projects that I'm interested are:

- Java - [Elasticsearch](https://github.com/elastic/elasticsearch): A distributed, RESTful search and analytics engine. Basically Google Search on your datasets. Very popular and active project. And I've seen it on job descriptions.
- Java - [UniversalMediaServer](https://github.com/UniversalMediaServer/UniversalMediaServer): A DLNA, UPnP and HTTP(S) Media Server. It seems active and looking for contributors. I'm interested in learning how to stream media over the network.
- Python - [Optuna](https://github.com/optuna/optuna): An automatic hyperparameter optimization framework, particularly designed for machine learning. I've used it before, and in theory is `for loops + cache`, but I would like to see how it works under the hood.
- Python - [Scrapy](https://github.com/scrapy/scrapy): a fast high-level web crawling & scraping framework. I'm interested in learning how to scrape data from the web.

# <a id=java-backend-developer-track></a>**3. Java Backend Developer track**

I've been working on the Java Backend Developer track on [Hyperskill](https://hyperskill.org/tracks/12). The objective is to be able to complete the following projects:

- Music Advisor Project
- Cinema Room REST Service Project
- Recipes REST Service Project

I've almost completed the first project, Music Advisor, which is a CLI application that uses the Spotify API to recommend music to the user. I've learned about the Spotify API, OAuth2, HTTP requests, JSON, and CLI applications. I've also learned about [structural desing patternt](https://refactoring.guru/design-patterns/structural-patterns) and I can't stop seeing them everywhere, (say SpringBoot is a Facade pattern for Spring).

Apart from that, I've been reviewing the basics of Java, and to be honest, I'm starting to like the language. I used on my first year of college and it left me a very bad taste. But as I learn more about the language, I'm starting to appreciate the abstractions of it, and all of that jargon (polymorphism, inheritance, encapsulation, etc) is finally starting to make sense.

Overall, I'm happy with the progress I've made this week, and I'm starting to feel more confident in my ability to learn and re-learn technical concepts.
