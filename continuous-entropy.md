theme: Ostrich, 1

# Fighting Continuous Entropy
## Adventures in Continuous Delivery

@garyfleming

^ My name is... I am a...
^ The talk is called Fighting Continuous Entropy. When I have a talk called something like that, I have to accept that some of the audience, maybe most of you, don't know what entropy is. So let's start with something not technical (in the software sense)

---

# What is Entropy?

> "a thermodynamic quantity representing the unavailability of a system's thermal energy for conversion into mechanical work, often interpreted as the degree of disorder or randomness in the system."

^ I'm sure that has cleared that up.
^ I'll try to explain but, if you're a physicist, you'll probably disagree. That's fine. I'm simplifying for the benefit of everyone else, which means I'm going to be a bit wrong.

---

# What is Entropy?

> "Disorder of a system"

^ This is the important part, thought I suspect still a little abstract: More disorder means more possible states of a system. Entropy of the universe ONLY increases. Same of any closed system.
^ TODO still not convinced by this

<!-- ---

# Systems

^ TODO Does defining systems actually help? Taking it out for now.
^ Where parts come together to do something that the individual parts couldn't
^ TODO this is a crappy definition of a system. Tighten it up. -->

---

# System Experiment: Fishes

^ Imagine a polystyrene box. Place in it a piece of fish. Pack it up with ice. What happens?
^ It depends.
^ TODO IMAGES

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

# Multi-faceted

![ ](images/yarn.jpg)

^ We need to realise that there's no single solution to this problem. There are many. The best way of keeping our code living longer is to employ an arsenal of tooling, targeting different areas and different problems.

---

# Problem
## Knowing whether your software is releasable

^ Let's start with something that I'm hoping is very familiar. An easy starter.
^ If we want to know whether our software is starting to rot, the easiest thing we can do is release it. If we can release it frequently, we've got a really good starting point.

---

# Brief Intro to CI/CD

Continuous integration: All developers merge their code to a shared mainline at least once a day.


^ Like I say, this should be familiar to many so I won't be spending a great deal of time on it.
^ Continuous Integration... Build server ensures correctness. This pushes people towards good, advanced practice like Trunk Based Development. Problems come to light faster. This is a good thing. It's GOOD that you're suddenly getting a lot of merge conflicts -> Design conversations early. Rather than merge hell later.

---

# If it hurts, do it more often.

^ TODO consider pulling up to after multi-faceted/before the first problem
^ First read this mantra in Continuous Delivery (Humble, Farley). And it's the key revelation behind most of the practices I'll mention today: if something hurts, do it more often. You'll figure out your options for making it not hurt. For making it mundane. Boring.

---

# Brief Intro to CI/CD

## Continuous Delivery: all changes go to production; safely, quickly, and sustainably.

^ The gold standard here is that every commit that makes it through a CI build should be pushed to production. That can lead to hundreds of releases a week. Again, this
will generally be augmented by using build pipelines that check software is working, as well as practices like blue-green releases for zero downtime deploys.
^ The fact is that the peer-reviewed research in this space shows that teams that learn to do this delivery services faster and more reliably.

---

# Problem
## Dependency Updates

^ Dependencies are a key part of code rot. If you don't update them, many will start to cause issues, whether through lack of support, vulnerabilities, or just how they interact with the platforms they run on. It's essential that we take updates.
^ But it's hard. We tend to do it infrequently, every few months to a year. Because we don't do it that often, it's painful: lots of incompatibilities and tangles all at once.

---

# If it hurts, do it more often.

^ We know what we need to do. We need to do it more often. Instead of doing it on a near annual cycle, what if we did it nearly daily?
^ But how? This is not really something people do that often, at least intentionally. There is very little tooling for it. No named practices

---

^ TODO acknowledge that dependencies are a key part of code rot. Make sure you store the dependencies you need (go light on this section). Not enough. They will have gained security vulnerabilities and patches, and become incompatible with outer layers - but taking updates is painful (ask how often people update dependencies?) -- This is the core problem. What happens if we did this way more often? Like Daily. (if it's hard do it more often)

---

# Experiment: Dependency Update Daily

* Update
* Build and test
* Commit/Revert
* Commit causes CD to happen

^ The team I wanted to experiment with on this were using Spring boot so I found some basic Gradle tooling that would update all dependencies to their latest versions. "use-latest-versions"
^ I then challenged a team to make a build job that would run once a day, at say noon, that would update (update all, build/test, commit/revert)

---

# Outcome: Dependency Update Daily

Mostly success!

* Some Major Version upgrades would need intervention,
* Temporary exclusions are important,
* Found unexpected end-to-end issues!

^ Learned some valuable lessons: mostly worked. Some Major version number changes would need manual intervention. Temporary exclusions were important. Spring security header change caused end-to-end issues. Quick to spot, easy to undo.

---

^ TODO ancillary stuff: other exclusions around potential attack vectors, or major versions, libraries being abandoned (Hystrix)
^ TODO great automated tests are essential! All levels: unit, integration, end-to-end (mention spring security header upgrade issue)


---

## Continuous Regeneration

![](images/regen.jpg)

^ I was going to call this idea of keeping your dependencies updated "Continuous Regeneration". The slide basically writes itself. Dr Who regenerating! I was chatting this through with a few folk at a conference in November:, and someone rightly pointed out that maybe regeneration was a bad idea. Dr Who only regenerates every 2-4 years, in a fairly unpredicable. Not very continuous.

---

## Continuous Rejuvenation

![right](images/rejuvenation.jpg)

^ So instead, I'm calling it Continuous Rejuvenation. Just as we shouldn't let stress and problems pile up for months before treating ourselves, how about we do do the same for our systems? Just a little bit of rejuvenation every day... to stave off the fish from rotting.

---

# Dependency Updates: Other languages

* Single versioned: Maven, Gradle, packages.config
* Ranges and Lock files: gem/bundler, most JS frameworks.
* Possibly open: pip, some JS frameworks, gem

^ Clearly I can't be exhaustive about other languages and tools. There are too many variants.
^ Singled versioned: one definitive version (3.1.4). Usually requires tooling that can check for updates and modify the dependency file with new versions. Some tooling already exists but YMMV. Good news: it just takes one of you to do this and open source it.
^ Lock filed: open ranges (>=3.1.4) in one file, but running it creates a lock file. These tend to be easy: delete the lock file! Also want tooling to expand the ranges every once in a while (but less often)
^ Possibly open: don't require a version. Easy (re-run) but dangerous: hard to reproduce environment when things go wrong. Most have some optional lock file. Use it!

^ TODO can't be exhaustive here, but maybe reference Python, Ruby, and JS. Most languages have some dependency file or a dependency file and a lock file. If the former, need an update mechanism. If the latter, just blow away your lock file. Consider how you'll manage exclusions.

---

# Always use a Lock file!

^ This is worth calling out. If you have open ranges and a lock file, *always* use and commit the lock file. The number of "it works on my machine" arguments I've seen (particularly in JS spaces) that came down to poor lock file/dep management is pretty absurd.

---

# Next Layer: Runtimes

^ TODO JVM version, NPM version, Ruby version. Consider using intermediary tooling like Jabba, RVM etc to allow you to test on newer versions. Need to be able to safely rollback to old version somehow.

---

# Language Upgrades

^ TODO closely related to runtime but not identical. In particular think about big breaking changes. Python 2 -> 3: still not settled. Some orgs have many Python 2 apps so cost of change is high, plus some of those apps no longer have organisational understanding (more later). This is hard.

---

# VMs, Servers, etc

^ TODO problems here: long-lived VMs and servers get ad-hoc patches or break in subtle ways (network card)
^ TODO infrastructure as code, phoenix architecture, serverless etc

---

# Language Trends/Obsolescence 

^ TODO languages, eventually, fall out of favour. COBOL. FORTRAN. PERL. This is big. Hard. How do we avoid slipping into obsolescence?

---

# Problem
## People Come and Go.

^ 
^ TODO People will come and go. New people need to get up to speed. Teams will come and go. How do you make it resilient? How do you know when to stop/change?

---

# If it hurts, do it more often.

---

# Practice and Prepare for Perfect People

^ TODO make these points into slides
^ Do retros on it: How would we onboard a new developer? What's different or interesting about our process and tools? What stories do we have that makes us us?
^ Have tools that can take a new dev machine from zero to ready. Practice by wiping someone's machine every week.
^ Use techniques like example mapping and user story maps to bring people into your domain quickly.

---

^ TODO general todo: make sure we're repeating the adage of "if its hard do it more"

----

^ TODO conclusion: make no mistake, no matter what you do, the fish *will* rot. Entropy is inevitable.


---

# Thank You

![inline](images/cat3.gif)

@garyfleming
