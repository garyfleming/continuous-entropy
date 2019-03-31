theme: Posterish

# 1995

^ The year is 1995. This is where out story begins. Since some of you may not remember 1995, let me tell you about it...

---

# 1995

![left](images/netscape.svg)

^ Netscape Navigator was recently released and was the dominant web browser in the world.

---

# 1995

![left](images/goldeneye.jpg)

^ After the longest gap in Bond filming history, the franchise returned with Pierce Brosnan in Goldeneye. Definitely the best film, and later easily the best film to videogame adaptation.

---

# 1995

![left](images/marvel.jpg)

^ And, you might remember from this year's documentary, Captain marvel was running around, hunting down Skrulls. But she is not the hero of today's story... no, that would be Nigel.

---

# 👨🏻‍🦳  


^ Nigel works for a large company who do... it doesn't really matter what, bring a key piece of their tech stack in-house, having outsourced it for years. It collates a bunch of data and generates a document once a day. In the header for this document is a date in long written out format.

---

## November Fifteen, Nineteen Ninety-Five

^ Nigel thinks this is fine. The problem is... there's a typo. Rather than sixteen, someone spelt it differently...

---

## Sixteen =>
## Soxteen

^ Soxteen. The bigger problem is that the company weren't able to get the source code to make a fix. So every day, on the soxteenth day of the month Nigel ran a manual process to fix it: he'd print out the document, manually correct it, and scan it back in.
^ That meant for over 20 years someone, Nigel, had to be free on the soxteenth of the month to make a fix. He'd arrange their holidays around it. When it was a weekend, he'd come in.

---

## Sixteen =>
## Soxteen

^ Now that was awful, but tenable, for a while. For 20 years this happened, in the bowels of the company, far from anyone who could make a change. Until 21 years rolled around, Nigel did this task. Anyone who has done the date calculation in their head knows what 21 years after 1995 is...

---

# Two Thousand Soxteen

^ ... and so it went from a monthly workaround to a daily workaround. That... was less tenable.

---

* No source code (written in an older language)
* Runs in a green screen terminal,
* Has to be emulated.

^ The large company didn't have the source code, and the platform it ran on was long out of support. Options were limited, and the company was suddenly and unexpectedly in crisis. Nigel was worried.

---

## Fighting Continuous Entropy
### Adventures in Continuous Delivery
### @garyfleming

^ My name is... I am a...
^ The talk is called Fighting Continuous Entropy. When I have a talk called something like that, I have to accept that some of the audience, maybe most of you, don't know what entropy is. So let's start with something not technical (in the software sense)

---

# What is Entropy?

> "a thermodynamic quantity representing the unavailability of a system's thermal energy for conversion into mechanical work, often interpreted as the degree of disorder or randomness in [a closed] system."

^ I'm sure that has cleared that up.
^ I'll try to explain but, if you're a physicist, you'll probably disagree. That's fine. I'm simplifying for the benefit of everyone else, which means I'm going to be a bit wrong.

---

# What is Entropy?

> "Disorder of a closed system"

^ This is the important part, thought I suspect still a little abstract: More disorder means more possible states of a system. Entropy of the universe ONLY increases. Same of any closed system.

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

# Entropy in Software

^ So why have I been talking about entropy at all?
^ You might think that you write your software and put it into production and it'll remain the same forever. That's sadly not true. Code rots. It's a fish in a box, and the ice is melting.
^ What can we do to keep it cooler longer?

---

# 👨🏻‍🦳  

^ Nigel's problem was a fairly extreme case of this, so let's think about some problems that show entropy that might involve your day to day.
^ Let's use how a modern team might work to reflect on the problem's of the past.

---

# Multi-faceted

![ ](images/yarn.jpg)

^ We need to realise that there's no single solution to this problem. There are many. The best way of keeping our code living longer is to employ an arsenal of tooling, targeting different areas and different problems.
^ Originally I tried to create a layered model to think about this, but the truth is it's a lot messier than that.

---

# **Problem**
## Knowing whether your software is releasable

^ Let's start with something that I'm hoping is very familiar. An easy starter. When Nigel took over, they weren't really releasing the software any more, just running it. That makes things hard.
^ If we want to know whether our software is starting to rot, the easiest thing we can do is release it. If we can release it frequently, we've got a really solid base.

---

# Brief Intro to CI/CD

^ So, if we're going to be talking about frequent releases, we need to talk about Continuous Integration and Continuous Deployment. I don't want to spend too long on this part because, honestly, I see it as a baseline these days. If you're not already doing this, start there and don't worry about the rest yet.

---

# Continuous Integration

All developers merge their code to a shared mainline at __least__ once a day.

^ Just this practice accelerates teams
^ Continuous Integration... Build server ensures correctness. This pushes people towards good, advanced practice like TDD etc. Problems come to light faster. This is a good thing. It's GOOD that you're suddenly getting a lot of merge conflicts -> Design conversations early. Rather than merge hell later.

---

# Continuous Integration

Related:

* Trunk-Based Development
* Feature Toggles

^ Explain TBD. Opposite of branching. Faster, safer. Feature toggles.
^ TODO expand?

---

# If it hurts, do it more often.

^ First read this mantra in Continuous Delivery (Humble, Farley). And it's the key revelation behind most of the practices I'll mention today: if something hurts, do it more often. You'll figure out your options for making it not hurt. For making it mundane. Boring.
^ I want this stuff to be boring so I can focus my energy and excitement on customer stuff.

---

# Continuous Delivery

All changes go to production; safely, quickly, and sustainably.

^ The gold standard here is that every commit that makes it through a CI build should be pushed to production. That can lead to hundreds of releases a week. Again, this
will generally be augmented by using build pipelines that check software is working, as well as practices like blue-green releases for zero downtime deploys.
^ The fact is that the peer-reviewed research in this space shows that teams that learn to do this delivery services faster and more reliably.

---

# Continuous Delivery

Related: Blue-Green releases.

^ One way we can do CD safely is Blue/Green releases. We create two versions of our stack, whatever that might be, one is called blue and one is called green. When we do a release, traffic goes to blue, we upgrade green, and traffic starts switching over. If it all goes well, all traffic continues, and we upgrade blue. If goes badly, fail back
^ TODO image
^ TODO blue/green joke

---

# **Problem**
## Dependency Updates

^ Dependencies are a key part of code rot. If you don't update them, many will start to cause issues, whether through lack of support, vulnerabilities, or just how they interact with the platforms they run on. It's essential that we take updates.
^ But it's hard. We tend to do it infrequently, every few months to a year. Because we don't do it that often, it's painful: lots of incompatibilities and tangles all at once.

---

# If it hurts, do it more often.

^ We know what we need to do. We need to do it more often. Instead of doing it on a near annual cycle, what if we did it nearly daily?
^ But how? This is not really something people do that often, at least intentionally. There is very little tooling for it. No named practices

---

# Idea
## Update Dependencies Daily

^ So, what if we did our updates every day? We'd need some way of finding out which dependencies have newer versions, We'd need to apply those changes, and we'd need to find out whether it broke anything.

---

# Continuous Regeneration

![right](images/regen.jpg)

^ I was going to call this idea of keeping your dependencies updated "Continuous Regeneration". The slide basically writes itself. Dr Who regenerating! I was chatting this through with a few folk at a conference in November:, and someone rightly pointed out that maybe regeneration was a bad idea. Dr Who only regenerates every 2-4 years, in a fairly unpredicable. Not very continuous.

---

# Continuous Rejuvenation

![right](images/rejuvenation.jpg)

^ So instead, I'm calling it Continuous Rejuvenation. Just as we shouldn't let stress and problems pile up for months before treating ourselves, how about we do do the same for our systems? Just a little bit of rejuvenation every day... to stave off the fish from rotting.

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

# Dependency Updates: Other languages

* Single versioned: Maven, Gradle, packages.config

```
e.g
5.4.1
3.0-ALPHA
1.3.2
```

^ Clearly I can't be exhaustive about other languages and tools. There are too many variants. Instead focus on dependency styles.
^ Singled versioned: one definitive version. Usually requires tooling that can check for updates and modify the dependency file with new versions. Some tooling already exists but YMMV. Good news: it just takes one of you to do this and open source it.

---

# Dependency Updates: Other languages

* Ranges and Lock files: gem/bundler, most JS frameworks.

```
>=5.4.1
3.*
[3.7.1)
```

^ Lock filed: open ranges in one file, but running it creates a lock file. These tend to be easy: delete the lock file! Also want tooling to expand the ranges every once in a while (but less often)
^ A complication is that if you want to be able exclude dependencies, you're back to needing some kind of tooling.

---

# Dependency Updates: Other languages

* Possibly open: pip, some JS frameworks, gem

```
some-dep
a-different-dep
```

^ Possibly open: don't require a version. Easy (re-run) but dangerous: hard to reproduce environment when things go wrong. Most have some optional lock file. Use it!

---

# Always use a Lock file!

Avoid "It works on my machine"

^ This is worth calling out. If you have open ranges and a lock file, *always* use and commit the lock file. The number of "it works on my machine" arguments I've seen (particularly in JS spaces) that came down to poor lock file/dep management is pretty absurd. By commit time, we should have single-version!


---

# Good Tests are Essential!

^ TODO IMAGE pyramid?
^ If you're going to try this, or in fact, just about any major continuous effort, it forces you to improve your technical practices. You have to write good, appropriate tests if you don't want to get stuck. That's at all levels: unit, integration, end-to-end
^ The team I was trying this out with found some really weird bugs when they upgraded one system in a microservice architecture and not the other, that would've really hurt them if they didn't have these tests.

<!--

^ TODO ancillary stuff: other exclusions around potential attack vectors, or major versions, libraries being abandoned (Hystrix)
-->

---

# **Problem**
## Runtime Rot

^ Now Nigel's system ran on some old green screen runtime. It was obscure, even for the time. Moving it forward was extremely difficult. You might this this wouldn't affect you, but... I think it does

---

# Rot Will Set In

* JVM
* .NET
* NPM version

^ These are tools around our code that are dependencies but not in the same way. They provide platforms for our code to run on. Moving forward here is something we do rarely. Partly because the rate of change tends to be a bit slower, but also because it can be painful.
^ That said, the trend in platforms is to speed up. Java, for example, has gone from a major release every 3-4 years to every 6 months.

---

# The Continuous Now

^ We're seeing this more and more, across browsers, and platforms. There is only now. There is only current, and continuous. Do you even know what version of Chrome or Firefox you use? You use IE?... that's a shame.

---

# Intermediary Tooling

* Java -> Jabba
* Ruby -> RVM
* Python -> Virtualenv (to some degree)

^ If your platform doesn't have the ability to easily switch versions (NPM is good here), then consider using an intermediary. Something that lets you run a job where you can easily install and test an upgrade of a new runtime, and safely switch back when it fails. Because it will sometimes.


<!-- ---

# **Problem**
## Language Schisms

^ TODO closely related to runtime but not identical. In particular think about big breaking changes. Python 2 -> 3: still not settled. Some orgs have many Python 2 apps so cost of change is high, plus some of those apps no longer have organisational understanding (more later). This is hard. -->

---

# **Problem**
## Standing Servers

^ Another issue that would stop Nigel from moving things forward was that everything in the stack was fixed. It was running in a long-standing server. It was flaky.

---

# **Problem**
## Standing Servers

^ Long-lived servers will develop issues. This is inevitable. It doesn't matter whether they're real or virtualised. This could be because of admins or developers making adhoc changes that aren't consistent, or it could be because of hardware breakdown (have you any idea how irritating it is to fix a long-lived server when it turns out the network card has broken? It's not fun.)


---

# Avoid Snowflake Servers

* Hard to Reproduce
* Hard to Modify
* Require manual processes, auditing, and docs.

^ Named by Fowler. We know that most long-lived servers are snowflakes. We think we understand them and their uniqueness, but they're almost impossible to recreate. Our test environments and production envs tend to be different. Modifications are hard because we're only guessing at current state. They require laborious process. I don't want that.

---

# If it hurts, do it more often.

^ This is a space we're getting better at, but we don't do often enough because it can be a lot of work...
^ And we know by know, that it if hurts we should do it more often.

---

# Infrastructure as Code

* Chef/Puppet/Ansible
* Terraform
* Containerisation
* Various cloud toolkits

^ Thankfully, tooling is great in this space. We can use some tools to define what we want from our servers. We can use Containerisation like Docker to isolate our app from our servers to move forward more often. We can script what we want from cloud platforms.
^ TODO go longer on each of these

---

# Engineering practice

* Daily Deletion
* Chaos Engineering
* Dev Laptop Wipes

^ We can marry those tools to interesting engineering practices that encourage us to get used to change. We can tear down environments on a daily/weekly basis so that we know our tools are in a good state (and changes are made via them).
^ We can use chaos engineering (deleting, removing services in production) to ensure we have repeatable and resilient environments.
^ We can wipe a dev environment a week, to ensure that we get back at automating them.
^ TODO think of another engineering practice here, and move dev laptop wipes to the people section

---

# Caution: Take the Updates

^ If we're deleting environments frequently, it's worth also taking things like OS updates as part of that. It lets us ensure we are not stuck in an environment that is rotting away.

---

# **Problem**
## Languishing Languages

^ Despite the fact the source code was gone, Nigel's system would've been hard to upgrade anyway. It was written in a language that is rarely used these days called Delphi. Anyone know Delphi?

---

# **Problem**
## Languishing Languages

^ See, that's the problem. Hiring people who know Cobol, Fortran, Perl is hard and expensive (rare). Training them up is hard because people often don't want to. Keeping them is harder, because now they can go charge more elsewhere.

---

# Avoiding Obsolescence

* Move to new versions,
* Cautiously embrace new languages,
* Design language agnostic APIs


^ Move to new versions. Go to new languages cautiously (don't want to have a gazillion). Design APIs that can easily be reimplemented in other languages. Occasionally try it.

---

## Destroy Your Microservices

^ If we think that microservices are inherently replaceable, they should help us not fall into this language trap. You know that adage that your backups don't exist unless you deliberately practice restoring them? Your microservices aren't replaceable unless you deliberately practice rewriting them.

---

# **Problem**
## People Come and Go.

^ One thing that should worry you about Nigel's story is that there's just one of him. He has a truck factor of one. He could leave, he could get ill, many things could happen.

---

# **Problem**
## People Come and Go.

^ We know that people will come and go. That means knowledge leaving our teams, and people needing to get up to speed. Very few teams I see are any good at this. At best, teams tend to have a dev set-up script somewhere and then pair a bit, and at worst they newbie gets told to go read some documentation... for days. It's hard!

---

# If it hurts, do it more often.

^ So let's do it more often. Let's get used to this reality and figure out how to do better.

---

# **People Prepping**
## Retros

^ Do retros on it: How would we onboard a new developer? What's different or interesting about our process and tools? What stories do we have that makes us us?
^ Just telling these stories more often will make it easier to bring people in.
^ TODO longer on value.

---

# **People Prepping**
## Domain Knowledge

* User Story Maps
* Example mapping

^ Use techniques like example mapping and user story maps to bring people into your domain quickly.
^ TODO spend a minute talking about each of these

---

# **People Prepping**
## Staff Liquidity Matrices

^ Use liquidity matrixes to keep resiliency. If there are bits of knowledge or process in your teams that only one or two people know, then SLMs help visualise that. You can then choose to spread that information around by training more people up on it.
^ TODO add image
^ TODO more detail on what these are and how to use them

---

# **People Prepping**
## Bigger Changes

^ Dynamic reteaming by Heidi Helfand is a good book on how to utilise inevitable team change to your advantage. Go read it.
^ TODO slightly longer


---

# Everything is Rotting...

^ There are many, many directions and rabbitholes you can go down when you start on this kind of improvement journey because everything is rotting away. There are **many** more that I haven't listed. That can be overwhelming.

---

# ...You Can Get Better

^ You can get better. Sure, the proverbial fish in a box is rotting, but this is not a closed system. You can intervene.
^ Because the company that had Nigel worked for? That same company has since done almost all of the things I've been talking about. They're not perfect, but they're a lot better. You can be too.

---

# Thank You

## @garyfleming

![right](images/beautiful-fish.jpg)
