---
layout: post
title: RESTful URLs
state: published
---
What is a RESTful URI? What characteristics does it have that makes it so? Surely `GET /people/curtis` is better than `GET /getPeopleByName?name=curtis`, right?

Let's look at a better example:

![](/images/blog/restful_uris.PNG)

Which of the above ☝️ is a "RESTful" URI?

It comes from Stefan Tilkov's video on [REST: I don't Think it Means What You Think it Does][1]; and I think it is a fantastic question.

Most people, _myself included_, get it wrong. Which one do you think is right?
 
**My vote: #4**
 
How about you? **Vote now**!


...

...

...



The fact of the matter is that the question simply does not make sense.

> There is no such thing as a "RESTful URI"
>
> — _S. Tilkov_

# Diving deeper

If you look at the constraints specified by Roy Fielding, none of them directly focus on URIs. The closest would
be constraint #4, [Uniform Interface (Sec 5.1.5)][2].

Resources are identified in all requests; they are manipulated through representations; all communication is done via self-descriptive messages; and [hypermedia is the engine of application state][3].

Essentially, it is the _context_ through which URIs are presented and used which determines whether you are adhering to the constraint, rather than the URIs _themselves_.

A big part of understanding this requires understanding HATEOS. I think [Dan Palmer][4] does a great job providing an example on his blog post [Your API is not RESTful][5].

> “What do I need to know in advance to use this service?”. The correct answer is the domain, and the protocol. That’s all. Given that information, it should be possible to fully explore everything the service has to offer.
>
> — _D. Palmer_

He goes on to provide an example of how you can use Amazon via your browser, without ever being concerned about the specific URIs you utilize to buy your books or DVDs.

The same should go for your RESTful api. It doesn't really matter what your URI's actually are from a REST-perspective, as they are simply a means-to-an-end. The endpoints should not need to be documented to use them; rather, subsequent requests to an API should include and link to related resources, proving the means of navigation without any specific regard to the format of the identifiers.

[1]: https://youtu.be/pspy1H6A3FM?t=1083
[2]: https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#sec_5_1_5
[3]: http://www.peej.co.uk/articles/hypermedia-as-the-engine-of-application-state.html
[4]: https://danpalmer.me/
[5]: https://danpalmer.me/2015/01/your-api-is-not-restful
