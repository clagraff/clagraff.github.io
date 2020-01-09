---
layout: post
title: Darn Defaults
state: draft
---
I want to share a short tale about about an adventure with Java & Spring properties, in the hopes I can prevents others for falling for the same
issues my team did. This is a story about defaults-gone-wrong.

# The Setup

A little bit of background is needed to have a comprehensive picture. This story revolves around our Product API, our Authorization API, 
and the company's Authorization management system.

To keep things simple: the Product API allows clients to get product information, assuming they are authorized. The company's
authorization management system (auth system) is the source-of-truth on whether a client is authorized or not. The Authorization API
exists to mediate interactions between our Product API and this source-of-truth.

Why the middleman? The Authorization API supports an in-memory cache of authorized clients, as well as a database fallback which is
periodically updated. All in case the company's auth system in down or unavailable, which happens often.

So the auth flow is like this:

```
function isUserAuthorizedForResource(userID, resourceID) bool {
  var isAuthorized bool
  var err error
  
  isAuthorized, err = inMemoryCache.getAuthorization(userID, resourceID)
  if err == nil {
    // user was in our cache, return their auth state
    return isAuthorized
  }
  
  // user not in cache, check the auth system
  
  isAuthorized, err = authSystem.getAuthorization(userID, resourceID)
  if err == nil {
    return isAuthorized
  }
  
  // could not get to auth system, fall back to database
  isAuthorized, err = database.getAuthorization(userID, resourceID)
  if err == nil {
    return isAuthorized
  }
  
  // something really went wrong. cannot authorize user.
  return false
}
```
