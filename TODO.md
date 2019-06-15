# Possible TODOs.

Personal Feedback

* add https://blog.npmjs.org/post/185397814280/plot-to-steal-cryptocurrency-foiled-by-the-npm

* Make it less polemic. Use positive messages: make things dull and cosy so you can get better value.
* Consider cutting down the team stuff at the end
* Nail the landing better. The fish thing doesn't really work at the end.

* Use the shearing layers metaphor from How Buildings Learn.
* Different levels of change: code, libraries, runtimes (JVM), OS, etc. Security patches.
* Needs a degree of automation that most teams don't embrace.
* Must be easy and continuous, hence phrase _continuous rejuvenation_. Imagine a spa, nice bath, other self-care. Not necessarily daily, but frequently.
* Continuous Regeneration seemed like a good idea for a name: you can see the Dr Who slide... but that only happens every few years.
* Broken windows theory.
* Think about costs: do this might take a while to get right, but likely to be reusable (especially in a world where pipeline templates or software delivery machines can replicate change across projects)
* Think about costs of not doing it: wait for libraries to be quite far out of date, find it really painful to update, delay it, worsen the problem, less likely to do it again. IF things are painful we should do them more often.
* Bring in ideas like Biohacking: is it a good idea to put chips or implants in your body without knowing how you'll remove them or upgrade them? Kinda like taking a dependency. It has to be super easy, to the point of almost not noticing, for it to become worthwhile.
* Physical infrastructure will eventually break so migration plans need to exist.
* Cloud infrastructure will change at some point, so we need to be able to move. Whether we do this by migration plans, hexagonal architecture (for minimal lock-in), or a multi-cloud solution, that's up for grabs.
* People leaving or becoming knowledge silos is a very odd source of entropy. Can mitigate using staff liquidity matrixes.
* Often forgotten dependencies that need managed: SSL Certs need renewed, support infrastructure (Jenkins, Artifactory, Docker registry etc) needs the same level of care as the project itself.
* Hystrix being abandoned in favour of resilience4j. Still perfectly usable but bitrot will set in at some point. Won't embrace new ideas. Won't get better; calcified.
* How do we check that our libraries have stopped being maintained? Maybe they're just in a good state. Think about the update policies around this. "Check for updates daily. Tell me when something hasn't been updated for more than X months etc"
* Is there a correlation or connection between the entropy a library faces and the number of dependencies it has? The more numerous the dependencies, the more likely one is rotting.
* Story of open source libraries being stable and taken on by new maintainers who turn out to be malicious. A new, auto-ingested release would potentially go live automatically. Consider, though, that people generally wouldn't find these things regularly (basically no-one audits library code), the alternative is possibly the bigger case of living with large security vulnerabilities. https://www.schneier.com/blog/archives/2018/11/distributing_ma.html
* For the malicious update of Open Source libraries, from new maintainers, perhaps one mechanism for this is a more nuanced approach to dependency updates. Regular updates by long-term maintainers? Take them. Not update in a while and new maintainer? Hold off a while.
* For the malicious update of open source libraries, probably need to be doing vulnerability scanning anyway. Continuously.
* Found issues. Libraries that had lots of big breaking changes (maybe pause or avoid), libraries that had basically stopped being supported, tech choices that had been abandoned.
* chaos engineering for dashboards. CI jobs. Other infra
* The fact the JDK support model has changed. The fact that Java the language is moving forward aggresively
* "Unless you do something proactively to improve it, you get more of what you've already got". I'd say it's worse than that: entropy through e.g. meme copying rather than understanding means it will get worse. https://twitter.com/joe_jag/status/1083047296789630977
* consider the US government shutdown. Services that started failing due to lack of budget and/or automation. Example: ssl certs weren’t renewed in an automated manner and no-one could update
* Atomist is an interesting tool for dealing with this kind of entropy
* Python 2 to Python 3 is an interesting look at entropy. People reticent to move forward. Landscape fractured.
* Consider things like the legacy of Internet Explorer 6 through 9. Still out there in business of all sizes. Apps built for them doing crucial things have never been replaced. Weird economic factors. Momentum factors.
* Consider hamcrest. When Junit changed its dependency, hamcrest-core and hamcrest-library no longer made sense. https://exubero.com/2019/02/04/the-revivification-of-hamcrest/
* programmers as an outer shearing layer. Might suddenly find it hard to hire someone who knows your language (Python, say). What strategies do you deploy? Microservices (to aid rewrites), training etc
* Trisha gee on code rot (recompiling and testing a project that hasn't change in years): https://twitter.com/trisha_gee/status/1098191234726850561
* Dev machines: practice wiping them so they don't become a dependency
