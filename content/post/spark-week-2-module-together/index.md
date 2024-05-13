---
title: Encora Spark Week 2. Module together.
date: 2024-05-13
math: true
---

This week I finally met my team in their element, solving technical problems.

# Takeaways of the week

- It's time to master my tools
- The importance of communication
- Hacking solutions with my team

# Mastering my tools

I started this week with little on my plate, so I decided to explore some ideas from the book [_Apprenticeship Patterns_](https://www.oreilly.com/library/view/apprenticeship-patterns/9780596806842/). This book was recommended in a suggested reading from last week, and it seem to me that the **Spark** program its heavily influenced by it. The goal of the book is to share solutions to the dilemmas often faced by inexperienced software developers. The _Patterns_ in the name, mean the recurring solutions to a problem in a given context, in this case is related to motivations and morale of software Apprentices.

### What it means to be an Apprentice?

The book emphasizes that being an apprentice is about adopting an attitude of constantly thinking there is always a better/smarter/faster way of doing something. It depends in continuous learning. This phase is described to be an egoistical one, as it focuses on maximizing learning opportunities.

The book is themed around the concept of craftsmanship, and it's separated into modules that teach an specific solution. One of the initial problem that arised was "obtaining a job in the first place depends on your proficiency in a specific programming language".

I have a shallow understanding of many, and the book recommends to pick one, become fluent in it, and for the next few years use it to solve problems as my main language. The current market favors languages like Java, Kotlin, Go, and Javascript. Since I'm interested in distributed systems, I'm inclined to choose between Java and Go.

### Java re-visited

I picked the book [_Java in a Nutshell_](https://learning.oreilly.com/library/view/java-in-a/9781098130992/) to get up to speed on the language details. I've only read the first few chapters so far, and I learned how Java is considered a _blue collar_ programming language. It focuses on being human-readable, with c/c++ vibes, and is class/object based.

Its execution environment, the JVM, is piece of craft by itself. It is an OS process that runs the code in an isolated, empty virtual machine. Java code is converted into bytecode, which the JVM executes using an interpreter and a JIT compiler that optimize sections of code to highly performant machine code, bypassing the interpreter. The performance is so good that there are many programming languages with ports to the JVM and the Java Ecosystem, such as Kotlin, Scala, Clojure, etc.

Running multiple versions in my Intel chip MacOS was pretty straightforward. I installed the tar's of the OpenJDK versions into the directory `\Library\Java\JavaRuntime\` using the command

```bash
sudo tar xzf ~\Donwloads\openjdk-[version]
```

and to change between versions, I only need to change the environment variable using `export JAVA_HOME=\...\openjdk-[version]\contents\home`.

# The importance of communication

Communication was a recurring theme and a key takeaway from the various meetings I attended this week. The Operations Teams highlighted how a lack of clear communication can impact performance and client relationships. Uncertainty and room for interpretation should be minimized to maintain partnership with clients.
Responsability is not delegated.

Another aspect of effective communication is building community and creating safe spaces within a diverse large organization. Each individual brings their own perspective and reference system. What may seem evident to one person may not be clear to others. Empathy plays a crucial role here; it is important to ask questions and understand others' viewpoints rather than assuming or anticipating their thoughts or needs.

Lastly, I had the opportunity to meet with the Operational Communication teams and learn the different initiatives at Encora to mitigate communication barriers with clients.

# Hacking solutions with my team

We were assigned two hard leetcode problems, and two mediums, in four programming languages.

- [Median of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays/) _hard_
- [LRU Cache](https://leetcode.com/problems/lru-cache/) _mid_
- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) _mid_
- [Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/) _hard_

I must admit that I don't consider myself particularly strong in solving this type of problem under pressure, especially during interviews where I tend to overthink and overanalyze.

I will share my technical insights and solution in a separate post. For now, I want to highlight the benefits of attacking problems as a team. I found it incredibly enjoyable to collaborate with my teammates on these challenges. Communicating on a technical level helped me understand my teammates better and vice versa, as is our element. I could sense how their thought processes differed from mine, what nuances they paid attention to, and what they overlook. Similarly, they provided clarity on aspects that I tended to overlook.
