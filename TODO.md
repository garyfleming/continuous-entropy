# Possible TODOs.

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
