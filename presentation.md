class: center, middle

# The strangler pattern

## An Agile Approach to a Legacy System

[live presentation](http://alonisser.github.io/strangler-pattern-talk) <br/>
[twitter](alonisser@twitter.com), [medium](https://medium.com/@alonisser/)

#####Shameless promotion: you can also read my political blog: [דגל אדום](degeladom@wordpress.com)
---

# The big rewrite

Why?

--

* The classic reference Old and "unmaintainable" technology (c/stored procedurex/ no defined api / etc)

* App does not behave as we want and the current language/framework won't support the behavior we want.
 
* The original code does not allow us to extend and add new features.

* Hubris

---

# The big rewrite - the problems

--

* There is no direct business value!

--

* There can be only one - It's binary in nature, either we are with the new system or the old

--

* Can be extremely time consuming, in the meanwhile the old system also needs new features and changes, The rabbit never catches the turtle

--

* There is hidden functionality (sometimes even old bugs become features) we would discover only during the migration, we need a way backwards

--

* critical systems: Almost **every** software system is critical to the client

---

# Strangler to the rescue

* A strangler?

"One of the natural wonders of this area are the huge strangler vines. They seed in the upper branches of a fig tree and gradually work their way down the tree until they root in the soil. 
Over many years they grow into fantastic and beautiful shapes, meanwhile strangling and killing the tree that was their host."

---

# Strangler to the rescue

A strangler pattern:
 
 "gradually create a new system around the edges of the old, letting it grow slowly over several years until the old system is strangled"

---

# Pros for the strangler pattern:

* Value to share holders is evident much quicker

* No (less..) double coding of features

* Incremental releases - agile not waterfall.

---
# A simple use case

* Http based app (Url navigation)

* clear asset separation

* No need to maintain new data backwards (Or just a read side)

---
# A simple use case - Using a reverse proxy

### Using a load balancer/reverse proxy (Nginx for example) to redirect new paths

```
server {

  location / {
    pass_proxy old-app.example.com;
  }

  location ~ ^/cool-things {

    pass_proxy new-app.example.com;
  }

}
```

Pros: simple

Cons: Isn't enough to handle write actions by it self, Can not differentiate by user/rules, limited configuration

---

# A simple use case - Using a "routing app"

### All traffic goes through a simple "bare bones" routing app (Or API Gateway)

pros:
 
* can route by url/user/site/origin/any other rule you device

* Ability to test new production code, before rolling out to end users.

---

# A simple use case - Using a "routing app"

Lessons:

1. Start simple (route all traffic through to old app), find broken technical problems early.

2. Backward compatibility is important

---
# Bigger challenges

* Data replication: [Event Interception](http://www.martinfowler.com/bliki/EventInterception.html)

* If you are already using event based replication then everything is easier

* Migrating assets back and forth see [Asset Capture](http://www.martinfowler.com/bliki/AssetCapture.html)

---
# Even bigger challenges

* No Http url routing (Desktop apps for example) - This was the original test case

* Old and new systems living together with the same asset.

---

# Building for strangling

Remember: today We are building the legacy applications of the future.

--

How do we build for future strangling?

---

# More info

* [The original InkBlot article](http://cdn.pols.co.uk/papers/agile-approach-to-legacy-systems.pdf)
* [The strangler pattern definition](http://www.martinfowler.com/bliki/StranglerApplication.html)
* [Different strangler use cases](http://paulhammant.com/2013/07/14/legacy-application-strangulation-case-studies/)
* [Another strangler story](http://agilefromthegroundup.blogspot.co.il/2011/03/strangulation-pattern-of-choice-for.html)



---

class: center, middle

#Open source rocks!

---

class: center, middle

#Thanks for listening!

---
