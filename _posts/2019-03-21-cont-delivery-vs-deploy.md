---
layout: post
title: Continuous Deploy vs Continious Delivery
state: published
---
What is the difference between **Continuous Deployment** and **Continuous Delivery**?

They often get conflated when talking about a "CI/CD pipeline"; and honestly it wasn't something
I've stopped to consider before. The question seems easy to answer, but I wanted to make sure I did my research.

After all, semantics are important.

So... what better an opportunity to learn the differences than now?

# The general consensus

A solid article highlighting the differences is from [Atlassian][1], where the key distinction is that
continuous delivery means you can deploy changes to clients quickly and consistently, but _not_ necessarily automatically.

Continuous deployment, on the other hand, does goes the _extra step_ and deploys code to production once it has
passed through the CI pipeline. No manually triggering a deploy. If the code is green, it goes to prod.

I would personally argue that delivery ties into the idea of [always being shippable][2]; that you should be able to deploy at any time, not just frequently.


[1]: https://www.atlassian.com/continuous-delivery/principles/continuous-integration-vs-delivery-vs-deployment
[2]: https://dri.es/always-be-shippable
