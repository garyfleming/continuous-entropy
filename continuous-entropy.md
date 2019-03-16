theme: Ostrich, 1

# Fighting Continuous Entropy
## Adventures in Continuous Delivery

@garyfleming

^ My name is... I am a...
^ The talk is called Fighting Continuous Entropy. When I have a talk called something like that, I have to accept that some of the audience, maybe most of you, don't know what entropy is. So let's start with something not technical (in the software sense)

---

# What is Entropy?

> "Disorder of a system"

^ I'll try to explain but, if you're a physicist, you'll probably disagree. That's fine. I'm simplifying for the benefit of everyone else, which means I'm going to be a bit wrong.

---

# What is Entropy?

> "Disorder of a system"

^ Does that help? More disorder means more possible states of a system.
Entropy of the universe ONLY increases. Same of any closed system.

---

# Systems

^ Where parts come together to do something that the individual parts couldn't
^ TODO this is a crappy definition of a system. Tighten it up.

---

# System Experiment: Fishes

^ Imagine a polystyrene box. Place in it a piece of fish. Pack it up with ice. What happens?
^ It depends.

---

# System Experiment: Fishes and Time

* 10 minutes?
* 10 hours?
* 10 days?
* 10000 years?

^ time is a key component of understanding entropy in systems. We might know (to some degree) the state of a system at some point, but over time it will change. Consider our fish box at these time scales. 10 minutes? Probably much the same. 10 hours? Ice will be melting but fish might be fine. 10 days? Fish will be rotten. 10000 years? The box will have started to breakdown.

---

# Software and Entropy

^ TODO rename slide?
^ So why have I been talking about entropy at all?
^ You might think that you write your software and put it into production and it'll remain the same forever. That's sadly not true. Code rots. It's a fish in a box, and the ice is melting.
^ What can we do to keep it cooler longer?

---

# Different Levels/Layers

^ TODO cover the fact that it's important to realise that this is a layered problem.

---

# Intro to CI/CD

^ TODO The basics of CI/CD. Keep this section light. Should be enough to bring people on the journey and no more. Introduce the idea that if something is hard we should do it more often.

---

# Core problem: Dependency Updates

^ TODO acknowledge that dependencies are a key part of code rot. Make sure you store the dependencies you need (go light on this section). Not enough. They will have gained security vulnerabilities and patches, and become incompatible with outer layers - but taking updates is painful (ask how often people update dependencies?) -- This is the core problem. What happens if we did this way more often? Like Daily. (if it's hard do it more often)

---

# The Experiment

^ TODO Quick prototype in Java that updates dependencies on command. Asked a team to experiment by making a build job (update all, build/test, commit/fail). Learned some valuable lessons: mostly worked. Some Major version number changes would need manual intervention (could be excluded temporarily) but at least we now knew this.
^ TODO ancillary stuff: other exclusions around potential attack vectors, or major versions, libraries being abandoned (Hystrix)
^ TODO great automated tests are essential! All levels: unit, integration, end-to-end (mention spring security header upgrade issue)

---

# Continuous Regeneration/Rejuvenation

^ TODO Explain the naming of this technique

---

# Other languages

^ TODO can't be exhaustive here, but maybe reference Python, Ruby, and JS. Most languages have some dependency file or a dependency file and a lock file. If the former, need an update mechanism. If the latter, just blow away your lock file. Consider how you'll manage exclusions.

---

# Next Layer: Runtimes

^ TODO JVM version, NPM version, Ruby version. Consider using intermediary tooling like Jabba, RVM etc to allow you to test on newer versions. Need to be able to safely rollback to old version somehow.

---

# Language Change

^ TODO closely related to runtime but not identical. In particular think about big breaking changes. Python 2 -> 3: still not settled. Some orgs have many Python 2 apps so cost of change is high, plus some of those apps no longer have organisational understanding (more later). This is hard.

---

# VMs, Servers, etc

^ TODO problems here: long-lived VMs and servers get ad-hoc patches or break in subtle ways (network card)
^ TODO infrastructure as code, phoenix architecture, serverless etc

---

# People

^ TODO People will come and go. New people need to get up to speed. Teams will come and go. How do you make it resilient?

---

^ TODO general todo: make sure we're repeating the adage of "if its hard do it more"

---

# Thank You

![inline](images/cat3.gif)

@garyfleming
