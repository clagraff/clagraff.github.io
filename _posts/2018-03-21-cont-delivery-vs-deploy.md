---
layout: post
title: Continuous Deploy vs Continious Delivery
state: draft
---
What is the difference between **Continuous Deployment** and **Continuous Delivery**?

They often get conflated when talking about a "CI/CD pipeline"; and honestly it wasn't something
I've stopped to consider before. Semantics are important, so what better an opportunity to understand the differences than now?

# The general consensus

A solid article highlighting the differences is from [Atlassian][1], where the key distinction is that
continuous delivery means you can deploy changes to clients quickly and consitently, but _not_ necessarily automatically.

Continuous deployment, on the other hand, goes the _extra step_ and deploys code to production once it has successfully
passed through the CI pipeline. No manually triggering a deploy. If the code is green, it goes to prod.

I would argue that delivery ties into the idea of [always being shippable][2] moreso than deployment does.


# But wait, there's more!

The internet is a big place; and as such, you can find a lot of varying opinions on the subject.

There are some who [advocate][2] that continuous delivery is simply about being able to deploy at any
time, but not automatically. The difference is minor, but important. It ties into the idea of [always being shippable][3], where 
it isn't enough to be able to deploy frequently and reliably; you should _always_ be able to deploy. At any time.






Firstly, there are those who believe the words are completely interchangable.

[1]: https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment
[2]: https://dri.es/always-be-shippable
