---
layout: post
title: Darn Defaults
state: draft
---
I want to share a short tale about about an adventure with Java & Spring properties, in the hopes I can prevents others for falling for the same
issues my team did. This is a story about defaults-gone-wrong.

# The Setup

A little bit of background is needed to have a comprehensive picture. This story revolves around our `Product API`, our `Authorization API`, 
and the company's `Authorization Management System` or `ams` for short.

The `Product API` is how clients interact with product data, assuming they are authorized.
The company's `ams` is the source-of-truth on whether a client is authorized or not. The `Authorization API` exists
to mediate interactions between our Product API and this source-of-truth.


The `Authorization API` supports an in-memory cache of previously authorized clients, and a database fallback in case 
the cache is empty _and_ `ams` is down.

So the auth flow is like this:

```go
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
