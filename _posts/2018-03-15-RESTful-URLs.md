---
layout: post
title: RESTful URLs
state: draft
---

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

A big portion of understanding this requires understanding HATEOS. I think [Dan Palmer][4] does a great job providing an example on his [blog post][5]:

> If we think about it, this is exactly how the web works. To use “Amazon”, I have to know that it lives at `amazon.com`, and that I can communicate with it over HTTP. To browse the service, I can load up `amazon.com`, and it will present me with a range of links to other resources I can go to, for example Books and DVDs, and a list of actions I can take as forms, such as searching or logging in. I didn’t need any documentation to tell me that to search I had to go to `/search?q=something`, and I didn’t need to be told that books were at `/products/books`.

[1]: https://youtu.be/pspy1H6A3FM?t=1083
[2]: https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm#sec_5_1_5
[3]: http://www.peej.co.uk/articles/hypermedia-as-the-engine-of-application-state.html
[4]: https://danpalmer.me/
[5]: https://danpalmer.me/2015/01/your-api-is-not-restful
